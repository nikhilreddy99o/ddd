Subject: Aqua Scan Results – Prometheus and Grafana

Hi Sergio,

Please find below the Aqua scan results for the Prometheus and Grafana images:

Prometheus:
A total of 5 vulnerabilities were found.

| Vulnerability       | GIS Severity        | Aqua Severity | Resource Name    | Resource Version | Resource Type |
| ------------------- | ------------------- | ------------- | ---------------- | ---------------- | ------------- |
| CVE-2025-22870 (x2) | Priority 3 - medium | medium        | golang.org/x/net | 0.35.0           | go package    |
| CVE-2023-42365      | Priority 4 - low    | medium        | busybox          | 1.36.1           | executable    |
| CVE-2023-42364      | Priority 4 - low    | medium        | busybox          | 1.36.1           | executable    |
| CVE-2023-42363      | Priority 4 - low    | medium        | busybox          | 1.36.1           | executable    |

Grafana OSS 10:
1 vulnerability found.

| Vulnerability  | GIS Severity        | Aqua Severity | Resource Name             | Resource Version | Resource Type |
| -------------- | ------------------- | ------------- | ------------------------- | ---------------- | ------------- |
| CVE-2025-30153 | Priority 3 - medium | high          | github.com/getkin/openapi | 0.120.0          | go package    |

Detailed scan reports are attached for your reference.
Additionally, we have removed the old image from FROG.

Thanks, Chandra, for your support in each request.

@Paula: When you have time, could you please download the necessary plugins from Grafana? We are currently unable to do so due to GIS security restrictions. Once downloaded, we can enable them on our side. We’ll also let you know if any additional plugins are needed. Other teams across the bank are following the same approach, and Grafana support also confirmed this process.


