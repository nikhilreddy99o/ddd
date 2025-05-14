[Convert]::ToBase64String((Get-Content -Path ".\trino-datasource-1.0.11.zip" -Encoding Byte)) > trino-plugin.b64
