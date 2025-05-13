Subject: RE: Access/Permissions AMI Prod

Hi Greg,

Could you please help me with this ticket?

I have added full SELECT roles to the following:

* `ami_workspace_iceberg`
* `ami_card_reporting`
* `merch_by_gen_aggr_ice_mtlzd`

I also tried creating a test materialized view using:

```sql
SHOW CREATE MATERIALIZED VIEW "ami_workspace_icebergs"."ami_card_reporting"."merch_by_gen_aggr_ice_mtlzd" LIMIT 10;
```

I attempted this through both BIAC and manual steps, but nothing seems to work. I successfully created a test view, but while `piram` can access it, I am unable to access the same view (`merch_by_gen_aggr_ice_mtlzd_test1`).

Even after trying all steps, I still encounter the following error:
**Access Denied: View owner does not have sufficient privileges. View owner 'nbk5yxb' cannot create a view that selects from `ami_workspace_iceberg`, `ami_card_reporting`, or `merch_by_gen_aggr`.**

Additionally, I’m able to access all three views when using `rd` but encounter this issue while accessing from `zsbidcp3`:

* I **cannot access**: `merch_by_gen_aggr_ice_mtlzd`, `merch_by_gen_aggr_ice_mtlzd_test`
* But I **can access**: `merch_by_gen_aggr_ice_mtlzd_test1`

Could you please advise?

Thanks,
Nikhil
