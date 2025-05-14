[System.Text.Encoding]::RegisterProvider([System.Text.CodePagesEncodingProvider]::Instance)
[Convert]::ToBase64String([IO.File]::ReadAllBytes(".\trino-datasource-1.0.11.zip")) | Out-File -Encoding ASCII trino-plugin.b64


