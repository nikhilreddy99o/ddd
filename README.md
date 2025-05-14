

Hi,

We have already identified this issue in the `ami_prod` environment. When a prod restart is performed, the log gets cleared, and there’s no issue. However, since we cannot perform regular restarts in production, we are planning to address this at the database level, not through configuration changes.

So, even if we increase the value, the log will eventually fill up again.
If you just reload and continue certain actions like changing roles or saving queries, it should function properly and complete within a maximum of 5 minutes.

I will discuss with Rai to determine if we should consider increasing the CPU on the DBs.

Regards,
Nikhil Karra
Bank of America

