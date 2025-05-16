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
              ls -la /plugins/trino && \
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
              value: /plugins/trino
          volumeMounts:
            - name: trino-plugin-volume
              mountPath: /var/lib/grafana/plugins/trino
            - name: grafana-config
              mountPath: /etc/grafana/grafana.ini
              subPath: grafana.ini

      volumes:
        - name: trino-plugin-volume
          emptyDir: {}
        - name: grafana-config
          configMap:
            name: grafana-smtp-config

      imagePullSecrets:
        - name: ebit-nonprod-registry
