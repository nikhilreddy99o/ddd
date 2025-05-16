
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
  namespace: cp-5670375  # Ensure correct namespace
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
          command:
            - sh
            - -c
            - |
              echo "Starting Trino plugin download..." && \
              mkdir -p /plugins/trino && \
              echo "Downloading plugin from SharePoint..." && \
              curl -L -o /plugins/trino/trino-plugin.zip "?...&download=1" && \
              echo "Download completed. Extracting plugin..." && \
              unzip -o /plugins/trino/trino-plugin.zip -d /plugins/trino/ && \
              echo "Extraction complete. Verifying contents..." && \
              ls -l /plugins/trino && \
              echo "Trino plugin setup completed successfully."
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

