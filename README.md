apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
  namespace: cp-5670375
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      initContainers:
        - name: download-trino-plugin
          image: curlimages/curl:latest
          command: ["/bin/sh", "-c"]
          args:
            - |
              echo "Starting Trino plugin download..." && \
              mkdir -p /plugins/trino && \
              curl -o /plugins/trino/trino-plugin.zip "" && \
              echo "Download completed. Extracting plugin..." && \
              unzip /plugins/trino/trino-plugin.zip -d /plugins/trino/ && \
              echo "Extraction complete. Verifying contents..." && \
              ls -l /plugins/trino && \
              echo "Plugin setup completed successfully."
          volumeMounts:
            - name: trino-plugin-volume
              mountPath: /plugins/trino

      containers:
        - name: grafana
          image: registry-nonprod.sdi.corp.bankofamerica.com/73708/monitoring/grafana-oss:10
          ports:
            - containerPort: 3000
          env:
            - name: GF_PATHS_CONFIG
              value: /etc/grafana/grafana.ini
            - name: GF_INSTALL_PLUGINS
              value: trino-datasource
          volumeMounts:
            - name: trino-plugin-volume
              mountPath: /var/lib/grafana/plugins/trino-datasource
            - name: grafana-config
              mountPath: /etc/grafana/grafana.ini
              subPath: grafana.ini
      volumes:
        - name: trino-plugin-volume
          emptyDir: {}
        - name: grafana-config
          configMap:
            name: grafana-config
      imagePullSecrets:
        - name: ebit-nonprod-registry
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
    admin_password = admin73708

    [smtp]
    enabled = true
    host = your-smtp-user
    user = your-smtp-user
    password = your-smtp-password
    from_address = grafana@example.com

    [plugins]
    allow_loading_unsigned_plugins = trino-datasource
