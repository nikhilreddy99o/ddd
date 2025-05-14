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
      containers:
        - name: grafana
          image: registry-nonprod.sdi.corp.bankofamerica.com/73708/monitoring/grafana-oss:latest
          ports:
            - containerPort: 3000
          env:
            - name: GF_PATHS_CONFIG
              value: /etc/grafana/grafana.ini
            - name: GF_INSTALL_PLUGINS
              value: trino-datasource
          volumeMounts:
            - name: trino-plugin-volume
              mountPath: /var/lib/grafana/plugins/trino-datasource-1.0.11.zip
              subPath: trino-datasource-1.0.11.zip
            - name: additional-volume-0
              mountPath: /var/lib/grafana
            - name: grafana-smtp-config
              mountPath: /etc/grafana/grafana.ini
              subPath: grafana.ini
      volumes:
        - name: trino-plugin-volume
          configMap:
            name: trino-plugin-config
        - name: additional-volume-0
          persistentVolumeClaim:
            claimName: grafana
        - name: grafana-smtp-config
          configMap:
            name: grafana-smtp-config
      imagePullSecrets:
        - name: ebit-nonprod-registry
