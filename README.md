In production, we're not allowed to delete or restart the pod related to audit logs until the release day. Our upcoming release is scheduled for May 9.

We already have the following setting enabled:
starburst.access-control.audit.enabled=true

When the log reaches its size limit, we encounter issues. My question is: if we increase the log size to 10,000, will it automatically delete or refresh the old logs?

This issue occurs only in production. In lower environments, everything is working fine.

Additionally, some tables and views were created in PROD using the ID NBK5YXB, but the service ID ZSBIDPC3 is unable to access the Materialized View (see screenshot below).
ZSBIDPC3 is able to query the table but not the view.
