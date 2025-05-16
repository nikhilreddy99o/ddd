apiVersion: v1
kind: ConfigMap
metadata:
  name: grafana-config
  namespace: cp-5670375
data:
  grafana.ini: |
    [server]
    http_port = 3000

    [auth]
    disable_login_form = false

    [security]
    admin_user = admin
    admin_password = admin123

    [smtp]
    enabled = true
    host =
    user = your-smtp-user
    password = your-smtp-password
    from_address = grafana@

    [plugins]
    allow_loading_unsigned_plugins = trino-datasource
