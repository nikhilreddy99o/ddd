{
  "name": "pystarburst_full_access",
  "description": "Full access role for PyStarburst usage",
  "users": ["user1", "user2", "user3", "user4"],
  "privileges": [
    {
      "catalog": ["*"],
      "schema": ["*"],
      "tables": ["*"],
      "action": ["*"]
    },
    {
      "category": "CATALOG_SESSION_PROPERTIES",
      "properties": ["*"],
      "action": ["SET"]
    },
    {
      "category": "SYSTEM_SESSION_PROPERTIES",
      "properties": ["*"],
      "action": ["SET"]
    }
  ]
}
