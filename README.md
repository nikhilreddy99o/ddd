import streamlit as st
import io
import sys
import traceback
import pandas as pd
from contextlib import redirect_stdout, redirect_stderr
from pystarburst import Session
from trino.auth import BasicAuthentication

# Streamlit page configuration
st.title("Python Terminal with Starburst Connection")

# Starburst connection details (from screenshot)
STARBURST_HOST = "gbt-edp-starburstdev..com"
STARBURST_PORT = 443
STARBURST_USER = ""
STARBURST_CATALOG = "hive"
STARBURST_SCHEMA = "default"

# Password input (since UI RBAC is assumed to restrict access)
password = st.text_input("Enter Starburst password:", type="password")

# Initialize Starburst session
@st.cache_resource
def get_starburst_session(_password):
    if not _password:
        return None
    try:
        session = Session.builder.configs({
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

# Text area for user code
user_code = st.text_area(
    "Enter Python code (use 'session' for Starburst connection):",
    height=300,
    placeholder="""e.g., 
df = session.sql('SELECT * FROM login_event_log LIMIT 5').collect()
print(df)
"""
)

# Run button
if st.button("Run"):
    if not user_code.strip():
        st.warning("Please enter some code to run.")
    elif not password:
        st.warning("Please enter your Starburst password.")
    else:
        # Capture output and errors
        output = io.StringIO()
        error_output = io.StringIO()
        
        # Get Starburst session
        session = get_starburst_session(password)
        if not session:
            st.error("Cannot execute code due to connection failure.")
        else:
            try:
                # Execute code in a standard Python environment
                globals_dict = {
                    "session": session,
                    "pd": pd,
                    "__builtins__": __builtins__  # Full Python terminal experience
                }
                
                with redirect_stdout(output), redirect_stderr(error_output):
                    exec(user_code, globals_dict)
                
                # Display output
                result = output.getvalue()
                if result:
                    st.success("Output:")
                    st.code(result, language="text")
                
                # Display DataFrame if created
                if "df" in globals_dict and isinstance(globals_dict["df"], pd.DataFrame):
                    st.subheader("DataFrame Result:")
                    st.dataframe(globals_dict["df"])
                
                if not result and "df" not in globals_dict:
                    st.info("Code executed successfully, but no output was produced.")
            
            except Exception as e:
                # Display detailed error with traceback
                error_trace = error_output.getvalue() + "\n" + traceback.format_exc()
                st.error("Error:")
                st.code(error_trace, language="text")
            
            finally:
                output.close()
                error_output.close()
                session.close()

# UI instructions and warnings
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
