import streamlit as st
import urllib3
import pandas as pd
import io
import sys
import traceback
from contextlib import redirect_stdout, redirect_stderr
from pystarburst import Session
from trino.auth import BasicAuthentication

# Disable SSL warnings
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Streamlit UI Title
st.title("Python Terminal with Starburst Connection")

# Starburst Connection Constants (corrected from screenshot)
STARBURST_HOST = "gbt-edp-starburstdev..com"  # Removed hyphen as per screenshot
STARBURST_PORT = 443
STARBURST_USER = ""  # Corrected from z to match screenshot
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
        }).build()  # Corrected to .build() as per pystarburst
        return session
    except Exception as e:
        st.error(f"Failed to connect to Starburst: {str(e)}")
        return None

# User Code Input Area
user_code = st.text_area(
    "Enter Python code (use 'session' for Starburst connection):",
    height=300,
    placeholder="""Example:
df = session.sql('SELECT DATE(created_at) AS date, COUNT(*) AS query_count FROM login_event_log WHERE created_at >= TIMESTAMP \\'2024-03-01\\' AND created_at < TIMESTAMP \\'2024-03-31\\' GROUP BY DATE(created_at)').collect()
avg_queries = df['query_count'].mean()
print(f'Average queries: {avg_queries}')
print(df)
"""
)

# Run Button
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

                # Display Output
                result = output.getvalue()
                if result:
                    st.success("Output:")
                    st.code(result, language="text")

                # Display DataFrame if exists
                if "df" in globals_dict and isinstance(globals_dict["df"], pd.DataFrame):
                    st.subheader("DataFrame Result:")
                    st.dataframe(globals_dict["df"])
                    # Add CSV Download
                    csv = globals_dict["df"].to_csv(index=False).encode('utf-8')
                    st.download_button(
                        "Download Data as CSV",
                        data=csv,
                        file_name='query_results.csv',
                        mime='text/csv'
                    )
                elif not result and "df" not in globals_dict:
                    st.info("Code executed successfully, but no output was produced.")

            except Exception as e:
                error_trace = error_output.getvalue() + "\n" + traceback.format_exc()
                st.error("Error:")
                st.code(error_trace, language="text")

            finally:
                output.close()
                error_output.close()
                session.close()  # Simplified, assuming session is valid

# UI Instructions
st.markdown("""
### Instructions:
- Enter your Starburst password to connect.
- Use `session` for Starburst SQL queries (e.g., `session.sql('SELECT ...').collect()`).
- This behaves like a Python terminal: imports, loops, functions, etc., are allowed.

#### Example:
```python
df = session.sql('SELECT DATE(created_at) AS date, COUNT(*) AS query_count FROM login_event_log WHERE created_at >= TIMESTAMP \\'2024-03-01\\' AND created_at < TIMESTAMP \\'2024-03-31\\' GROUP BY DATE(created_at)').collect()
avg_queries = df['query_count'].mean()
print(f'Average queries: {avg_queries}')
print(df)
