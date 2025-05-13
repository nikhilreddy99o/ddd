
Hi rai,

I have tested the Python UDF functionality, and it is available for version 468+. However, I observed some limitations:

* UDFs run in a restricted sandbox environment.
* They do not support external communications such as sending emails or accessing APIs.
* Complex processing and external integrations need to be handled via external scripts, such as using the **PyStarburst** client.

### Comparison:

| Feature      | UDF (User-Defined Function)              | PyStarburst (Python Client)                                     |
| ------------ | ---------------------------------------- | --------------------------------------------------------------- |
| Purpose      | Run small logic snippets inside SQL      | Run full Python scripts and connect to Starburst via API        |
| Execution    | Within Starburst SQL engine              | External Python environment                                     |
| Capabilities | Limited Python (no network/file access)  | Full Python capabilities (can send emails, access APIs, etc.)   |
| Use Cases    | Data transformation, simple calculations | Automate reporting, advanced data processing, trigger workflows |
| Limitations  | No external libraries, no I/O            | No limitations—depends on your Python setup                     |

Please let me know if you’d like me to explore further or set up a demo using PyStarburst for advanced use cases.

Thanks,
Nikhil Karra
