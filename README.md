Hi Paula,

I’m using GitHub Co-Pilot mainly for automation and development tasks. When I’m unsure about any logic or implementation, I leverage Co-Pilot’s chat feature for quick assistance. It also provides real-time auto-suggestions and auto-completion within the editor, which significantly speeds up my workflow.

Additionally, I often open server sessions directly from VS Code, and in those scenarios, I also use Co-Pilot to assist with writing and optimizing scripts on the server side. This helps streamline automation and reduce manual effort.

In compliance with our security guidelines, I make sure not to store any sensitive information (such as SSNs, passwords, keys, RBAC IDs, etc.) in tracked files. Sensitive data is kept in separate untracked folders to avoid triggering GIS security alerts and ensure Co-Pilot doesn’t access or feed on that information.

The Co-Pilot team is actively collaborating with the GIS team to address any related security triggers. Until then, we’re following the recommended best practices by excluding the following file types from being shared with Co-Pilot:

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

Please let me know if you’d like any further details.



