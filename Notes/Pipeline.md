## Jenkins Pipeline (Jenkinsfile)

Pipelines use CICD in code so no changes are required — automatable & sustainable with no manual steps.

```
Pipeline
    |
    +-- (i)  from built-in : Pipeline job (Jenkins pipeline)
    +-- (ii) Inline : Pipeline script in Jenkins pipeline
             |
             +-- approvals built-in
             +-- 4 plugins
```

### Pipeline Features:

| Feature        | Description                  | Chained Frestyle job                                     |  
|----------------|---------------------------------------|-----------------------------------------------|  
| **Code-as**    | One pipeline job in git,PR reviewed, versioned,Rollbackable                 | Logic scattered in UI, attack jobs, stale jobs               |  
| **Parallelism**   | Native parallel for fast, concurrent stages                           |        Required extra jobs/plugins; clunky to coordinate           |  
| **Conditionals**| When {} already goes by branch/tag/files                                 | Limited with duplicated jobs, params, gets messy                |  
| **Maintenance**| Minimal plugin-sprawl; One file the Per project; reliable via libraries     |  heavy plugin reliance; many jobs in maintenance;  |  
| **Approval/Input**| Built-in input step with timeouts/roles                                 | No native gate; rely on plugins or manual steps                 |  

