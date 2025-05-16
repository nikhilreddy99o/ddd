
Hi Paula,

I’m using GitHub Co-Pilot mainly for automation tasks. If I’m unsure about any logic or code, I utilize Co-Pilot’s chat for quick assistance. It also offers auto-suggestions and auto-completion directly within the editor, which helps improve efficiency.

In line with our security guidelines, I ensure that no sensitive information (like SSNs, passwords, keys, RBAC IDs, etc.) is stored in tracked files to prevent GIS security alerts. Sensitive files are maintained in a separate untracked folder, ensuring that Co-Pilot doesn’t access or feed on that content.

Additionally, the Co-Pilot team is actively working with the GIS team to resolve related security triggers. Until then, we’re following the recommended practices by excluding certain file types from being shared with Co-Pilot. Below are the excluded file types:

```
**/*.env  
**/*.csv  
**/*.properties  
**/*.ini  
**/*.dbf  
**/*.log  
**/*.xml  
**/*.config  
**/*.prop  
**/*.httpd  
**/*.httpx  
**/*.json  
**/*.yaml  
**/*.yml  
secrets.json
```

Please let me know if you need any further information.

Regards,
Nikhil Karra
Bank of America
Enterprise Business Intelligence Platforms – StarBurst (Trino)

---

Would you like me to make it even more concise, or add the reason why Co-Pilot requires these exclusions?
