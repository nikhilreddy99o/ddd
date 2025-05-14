df = session.sql("SELECT * FROM login_event_log").collect()
print(df)
