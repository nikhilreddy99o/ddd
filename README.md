apiVersion: v1
kind: ConfigMap
metadata:
  name: trino-plugin-config
  namespace: <your-grafana-namespace>  # Replace with correct namespace
data:
  trino-datasource-1.0.11.zip: |
    <Paste Base64 Content Here — Make Sure to Indent Each Line by 4 Spaces>
