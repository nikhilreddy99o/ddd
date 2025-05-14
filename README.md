Hi,

We have already identified this issue in the ami_prod environment. When a prod restart is performed, the log gets cleared, and there’s no issue. However, since regular restarts cannot be performed in production, we are planning to address this at the database level rather than through configuration changes.

So, even if we increase the value, the log will eventually fill up again. If you simply reload and continue actions like changing roles or saving queries, it should function properly and complete within a maximum of 5 minutes.

We are also considering increasing the CPU on the DBs.
