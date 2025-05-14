import streamlit as st
import urllib3
import pandas as pd
import io
import sys
import traceback
from contextlib import redirect_stdout, redirect_stderr
from pystarburst import Session
from trino.auth import BasicAuthentication

# Suppress SSL warnings
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Streamlit page title
st.title("Python Terminal with Starburst Connection")

# Starburst connection config
STARBURST_HOST = "gbt-edp-starburst-dev.bankofamerica.com"
STARBURST_PORT = 443
STARBURST_USER = "zkt44jo"
STARBURST_CATALOG = "hive"
STARBURST_SCHEMA = "default"

# Password Input
password = st.text_input("Enter Starburst password:", type="password")

@st.cache_resource
def get_starburst_session(_password):
    if not _password:
        return None
    try:
        session = Session.builder().configs({
            "host": STARBURST_HOST,
            "port": STARBURST_PORT,
            "http_scheme": "https",
            "auth": BasicAuthentication(STARBURST_USER, _password),
            "catalog": STARBURST_CATALOG,
            "schema": STARBURST_SCHEMA,
            "verify": False  # Not recommended for production
        }).create()
        return session
    except Exception as e:
        st.error(f"Failed to connect to Starburst: {str(e)}")
        return None

# Code Input Area
user_code = st.text_area(
    "Enter Python code (use 'session' for Starburst connection):",
    height=300,
    placeholder="Example:\ndf = session.sql('SELECT * FROM login_event_log LIMIT 5').collect()\nprint(df)"
)

if st.button("Run"):
    if not user_code.strip():
        st.warning("Please enter some code to run.")
    elif not password:
        st.warning("Please enter your Starburst password.")
    else:
        output = io.StringIO()
        error_output = io.StringIO()

        session = get_starburst_session(password)
        if not session:
            st.error("Cannot execute code due to connection failure.")
        else:
            try:
                globals_dict = {
                    "session": session,
                    "pd": pd,
                    "__builtins__": __builtins__
                }
                with redirect_stdout(output), redirect_stderr(error_output):
                    exec(user_code, globals_dict)

                result = output.getvalue()
                if result:
                    st.success("Output:")
                    st.code(result, language="text")

                # Display DataFrame if available
                if "df" in globals_dict and isinstance(globals_dict["df"], pd.DataFrame):
                    st.subheader("DataFrame Result:")
                    st.dataframe(globals_dict["df"])
                elif not result and "df" not in globals_dict:
                    st.info("Code executed successfully, but no output was produced.")

            except Exception as e:
                error_trace = error_output.getvalue() + "\n" + traceback.format_exc()
                st.error("Error:")
                st.code(error_trace, language="text")

            finally:
                output.close()
                error_output.close()
                try:
                    session.close()
                except Exception:
                    pass  # Session already closed or invalid

# UI Instructions
st.markdown("""
### Instructions:
- Enter your Starburst password to connect.
- Use `session` for Starburst SQL queries (e.g., `session.sql('SELECT ...').collect()`).
- This behaves like a Python terminal: imports, loops, functions, etc., are allowed.
- Example:
```python
df = session.sql('SELECT DATE(created_at) AS date, COUNT(*) AS query_count FROM login_event_log WHERE created_at >= TIMESTAMP \\'2025-03-01\\' GROUP BY DATE(created_at)').collect()
avg_queries = df['query_count'].mean()
print(f'Average queries: {avg_queries}')
print(df)
""")
