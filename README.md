{
  "roles": [
    {
      "name": "ami_power_users",
      "description": "AMI Power User",
      "groups": ["ami_sb_pwr-users_prod"],
      "privileges": [
        {
          "catalog": ["ami_object_storage", "ami_object_storage_iceberg", "aprtera", "iceberg_eit_object_storage", "ami_sb_insights", "ami_sqlserver_dbrfrl", "ami_workspace", "ami_workspace_iceberg"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["sdp_pthnrt_jdbc"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SHOW", "ALTER", "DELETE", "DROP", "REFRESH", "INSERT", "UPDATE", "CREATE"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_all_users",
      "description": "All AMI Users Read Only",
      "groups": ["ami_sb_auth_prod", "ami_sb_auth_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_public_space"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["sdp_pthnrt_jdbc"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT"],
          "effect": "ALLOW_WITH_GRANT_OPTION"
        },
        {
          "catalog": ["aprtera", "system"],
          "schema": ["builtin"],
          "function": ["query"],
          "action": ["EXECUTE"]
        },
        {
          "catalog": ["aprtera", "ami_sb_insights", "sdp_pthnrt_jdbc", "ami_sqlserver_dbrfrl"],
          "schema": ["system"],
          "function": ["query"],
          "action": ["EXECUTE"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_misn_cntrl_rw_prod",
      "description": "Mission Control Read/Write",
      "groups": ["ami_sb_misn-cntrl_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "iceberg_eit_object_storage", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_object_storage", "ami_object_storage_iceberg"],
          "schema": ["mission_control"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_mission_control"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_misn_cntrl_ro_prod",
      "description": "Mission Control Read Only",
      "groups": ["ami_sb_misn-cntrl_ro_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "iceberg_eit_object_storage", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_object_storage", "ami_object_storage_iceberg"],
          "schema": ["mission_control"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_mission_control"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_misn_cntrl_rw_serv_prod",
      "description": "Mission Control Read/Write for Service IDs",
      "groups": ["ami_sb_misn-cntrl_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "iceberg_eit_object_storage", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_object_storage", "ami_object_storage_iceberg"],
          "schema": ["mission_control"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_mission_control"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_misn_cntrl_ro_serv_prod",
      "description": "Mission Control Read Only for Service IDs",
      "groups": ["ami_sb_misn-cntrl_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "iceberg_eit_object_storage", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_object_storage", "ami_object_storage_iceberg"],
          "schema": ["mission_control"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_mission_control"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dat_rw_prod",
      "description": "Digital Analytics Tool Read/Write",
      "groups": ["ami_sb_dat_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dat"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_dat_ro_prod",
      "description": "Digital Analytics Tool Read Only",
      "groups": ["ami_sb_dat_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dat"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dat_rw_serv_prod",
      "description": "Digital Analytics Tool Read/Write for Service IDs",
      "groups": ["ami_sb_dat_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dat"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_dat_ro_serv_prod",
      "description": "Digital Analytics Tool Read Only for Service IDs",
      "groups": ["ami_sb_dat_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dat"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_ml_rw_prod",
      "description": "ML Automation and Visualization Read/Write",
      "groups": ["ami_sb_av-ml_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_ml"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_ml_ro_prod",
      "description": "ML Automation and Visualization Read Only",
      "groups": ["ami_sb_av-ml_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_ml"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_ml_rw_serv_prod",
      "description": "ML Automation and Visualization Read/Write for Service IDs",
      "groups": ["ami_sb_av-ml_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_ml"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_ml_ro_serv_prod",
      "description": "ML Automation and Visualization Read Only for Service IDs",
      "groups": ["ami_sb_av-ml_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_ml"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_csi_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_csi_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_csi_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_csi_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_cre_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_csi-cre_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi_cre"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_cre_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_csi-cre_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi_cre"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_cre_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_csi-cre_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi_cre"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_csi_cre_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_csi-cre_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["csi_cre"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_con_bnk_inv_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_con-bnk-inv_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["con_bnk_inv"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_con_bnk_inv_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_con-bnk-inv_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["con_bnk_inv"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_con_bnk_inv_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_con-bnk-inv_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["con_bnk_inv"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_con_bnk_inv_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_con-bnk-inv_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["con_bnk_inv"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_thoughtspot_rw_prod",
      "description": "Thoughtspot Read/Write",
      "groups": ["ami_sb_thoughtspot_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["thoughtspot"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_thoughtspot_ro_prod",
      "description": "Thoughtspot Read Only",
      "groups": ["ami_sb_thoughtspot_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["thoughtspot"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_thoughtspot_rw_serv_prod",
      "description": "Thoughtspot Read/Write for Service IDs",
      "groups": ["ami_sb_thoughtspot_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["thoughtspot"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_thoughtspot_ro_serv_prod",
      "description": "Thoughtspot Read Only for Service IDs",
      "groups": ["ami_sb_thoughtspot_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["thoughtspot"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_msmt_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_av-msmt_rw_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_msmt"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_msmt_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_av-msmt_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_msmt"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_msmt_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_av-msmt_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["aprtera", "ami_sb_insights", "ami_sqlserver_dbrfrl"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_msmt"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_msmt_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_av-msmt_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_msmt"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "sdp_sb_discovery_ro_prod",
      "description": "SDP read only role",
      "groups": ["sdp_sb_discovery_ro_prod"],
      "privileges": [
        {
          "catalog": ["sdp_pthnrt_jdbc", "sdp_prod"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT"],
          "effect": "ALLOW_WITH_GRANT_OPTION"
        },
        {
          "catalog": ["sdp_pthnrt_jdbc", "sdp_prod"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SHOW"]
        },
        {
          "catalog": ["blackhole_connector"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["sdp_pthnrt_jdbc", "sdp_prod", "blackhole_connector"],
          "schema": ["system"],
          "function": ["query"],
          "action": ["EXECUTE"]
        }
      ]
    },
    {
      "name": "sdp_sb_discovery_ro_serv_prod",
      "description": "SDP service read only role",
      "groups": ["sdp_sb_discovery_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["sdp_pthnrt_jdbc", "sdp_prod"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT"],
          "effect": "ALLOW_WITH_GRANT_OPTION"
        },
        {
          "catalog": ["sdp_pthnrt_jdbc"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SHOW"]
        },
        {
          "catalog": ["blackhole_connector"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["sdp_pthnrt_jdbc", "sdp_prod", "blackhole_connector"],
          "schema": ["system"],
          "function": ["query"],
          "action": ["EXECUTE"]
        }
      ]
    },
    {
      "name": "ami_sb_glbl_bnk_rw_prod",
      "description": "AMI global banking read/write",
      "groups": ["ami_sb_glbl-bnk_rw_prod"],
      "privileges": [
        {
          "catalog": ["ami_ora_sb_glbl_bnk_bgd", "ami_ora_sb_glbl_bnk_gwca"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        }
      ]
    },
    {
      "name": "ami_sb_glbl_bnk_ro_prod",
      "description": "AMI global banking read only",
      "groups": ["ami_sb_glbl-bnk_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_ora_sb_glbl_bnk_bgd", "ami_ora_sb_glbl_bnk_gwca"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_glbl_bnk_rw_serv_prod",
      "description": "AMI global banking read/write for service IDs",
      "groups": ["ami_sb_glbl-bnk_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_ora_sb_glbl_bnk_bgd", "ami_ora_sb_glbl_bnk_gwca"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        }
      ]
    },
    {
      "name": "ami_sb_glbl_bnk_ro_serv_prod",
      "description": "AMI global banking read only for service IDs",
      "groups": ["ami_sb_glbl-bnk_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_ora_sb_glbl_bnk_bgd", "ami_ora_sb_glbl_bnk_gwca"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_sbbb_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_sbbb_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sbbb"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_sbbb_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_sbbb_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sbbb"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_sbbb_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_sbbb_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sbbb"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_sbbb_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_sbbb_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sbbb"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_company_bridge_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_company-bridge_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_company_bridge"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_company_bridge_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_company-bridge_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_company_bridge"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_company_bridge_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_company-bridge_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_company_bridge"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_company_bridge_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_company-bridge_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_company_bridge"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_wb_rw_prod",
      "description": "Read/Write",
      "groups": ["ami_sb_wb_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_workplace_benefits"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_wb_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_wb_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_workplace_benefits"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_wb_rw_serv_prod",
      "description": "Read/Write for Service IDs",
      "groups": ["ami_sb_wb_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "wuatera", "rchtera", "wdvtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "sdp_dcon", "sdp_dcon_jdbc", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_workplace_benefits"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_wb_ro_serv_prod",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_wb_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_workplace_benefits"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_wb_ro_serv_uat",
      "description": "Read Only for Service IDs",
      "groups": ["ami_sb_wb_ro_serv_uat"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_workplace_benefits"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dda_vint_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_dda_vint_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sb_dda_vint"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dda_vint_rw_prod",
      "description": "Read/Write for smi_sb_dda_vint",
      "groups": ["ami_sb_dda_vint_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sb_dda_vint"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_dda_vint_ro_serv_prod",
      "description": "Read Only",
      "groups": ["ami_sb_dda_vint_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sb_dda_vint"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dda_vint_rw_serv_prod",
      "description": "Read/Write for smi_sb_dda_vint",
      "groups": ["ami_sb_dda_vint_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_sb_dda_vint"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_card_data_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_card_data_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_data"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_card_data_rw_prod",
      "description": "Read/Write for ami_sb_card_data_rw_prod",
      "groups": ["ami_sb_card_data_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_data"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_card_data_ro_serv_prod",
      "description": "Read Only",
      "groups": ["ami_sb_card_data_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_data"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_card_data_rw_serv_prod",
      "description": "Read/Write for ami_sb_card_data_rw_serv_prod",
      "groups": ["ami_sb_card_data_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_data"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_card_reporting_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_card_reporting_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_reporting"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_card_reporting_rw_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_prod",
      "groups": ["ami_sb_card_reporting_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_reporting"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_card_reporting_ro_serv_prod",
      "description": "Read Only for Service IDs with view access",
      "groups": ["ami_sb_card_reporting_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_reporting"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["merch_by_gen_aggr_ice_atid"],
          "tables": ["tat"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_card_reporting_rw_serv_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_serv_prod",
      "groups": ["ami_sb_card_reporting_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_reporting"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_cbi_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_av_cbi_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_cbi"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_cbi_rw_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_serv_dev",
      "groups": ["aami_sb_av_cbi_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_cbi"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_av_cbi_ro_serv_prod",
      "description": "Read Only",
      "groups": ["ami_sb_av_cbi_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_cbi"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_av_cbi_rw_serv_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_serv_dev",
      "groups": ["ami_sb_av_cbi_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_av_cbi"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_dspr_ro_prod",
      "description": "Read Only",
      "groups": ["ami_sb_dspr_ro_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dspr"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dspr_rw_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_serv_dev",
      "groups": ["ami_sb_dspr_rw_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dspr"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "ami_sb_dspr_ro_serv_prod",
      "description": "Read Only",
      "groups": ["ami_sb_dspr_ro_serv_prod"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dspr"],
          "tables": ["*"],
          "action": ["SELECT", "SHOW"]
        }
      ]
    },
    {
      "name": "ami_sb_dspr_rw_serv_prod",
      "description": "Read/Write for ami_sb_card_reporting_rw_serv_dev",
      "groups": ["ami_sb_dspr_rw_serv_prod"],
      "privileges": [
        {
          "catalog": ["teradata_apr_ts", "aprtera_jdbc", "dsp-mssql_digi_insight", "dsp-mssql_dbrfrl", "aprtera", "rchtera", "ts_sqlserver_dbrfrl", "ami_sqlserver_dbrfrl", "wuatera", "sdp_ucon", "sdp_ucon_jdbc", "ami_sb_insights", "wuatera_direct"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_dspr"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    },
    {
      "name": "cacheservice",
      "description": "cacheservice role for the cache serivce ID",
      "users": ["sersbrop"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        },
        {
          "category": "SYSTEM_SESSION_PROPERTIES",
          "properties": ["*"],
          "action": ["SET"]
        },
        {
          "catalog": ["*"],
          "schema": ["*"],
          "tables": ["*"],
          "action": ["*"]
        },
        {
          "catalog": ["system"],
          "schema": ["metadata"],
          "tables": ["*"],
          "action": ["*"]
        }
      ]
    },
    {
      "name": "public",
      "description": "Builtin role that is granted to all.",
      "privileges": [
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["query_max_cpu_time"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["query_max_run_time"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["query_max_execution_time"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["query_max_scan_physical_bytes"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["skip_results_cache"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["resource_overcommit"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["results_cache_entry_max_size_bytes"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["SET"],
          "entity_key": ["results_cache_key"],
          "category": "SYSTEM_SESSION_PROPERTIES",
          "all_entities": [false]
        },
        {
          "effect": "ALLOW",
          "action": ["EXECUTE"],
          "category": "QUERIES",
          "all_entities": [true]
        }
      ]
    },
    {
      "name": "ami_sb_card_reporting_view_creator",
      "description": "Role for creating materialized views in ami_card_reporting schema",
      "users": ["n"],
      "privileges": [
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["ami_card_reporting"],
          "tables": ["*"],
          "action": ["CREATE"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "schema": ["merch_by_gen_aggr_ice_atid"],
          "tables": ["*"],
          "action": ["SELECT"]
        },
        {
          "catalog": ["ami_workspace", "ami_workspace_iceberg"],
          "category": "CATALOG_SESSION_PROPERTIES",
          "properties": ["stale_materialized_view"],
          "action": ["SET"]
        }
      ]
    }
  ]
}
