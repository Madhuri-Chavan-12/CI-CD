# CI/CD (Continuous Integration / Continuous Deployment)



## 1. Continuous Integration (CI)

A development practice of integrating code into a shared repository. Each integration is verified by an **automated build** and **automated tests**.

### Aspects:
1. Develop & Compile
2. Perform Unit Tests
3. Integrate with DBs
4. Perform Production Deployment
5. Perform Functional Test & Code Labeling
6. Generate Reports & Analyze Code

---

## 2. Continuous Deployment (CD)

Aims to **reduce the time** the development team takes between writing a new line of code and using it in production.

- Highly automated process which increases accuracy
- Scripts take over manual work during deployment
- Scripts create the computing environment before deployment

### Tools:
> Jenkins, Travis CI, Bamboo, GitLab, Teamcity

---

## Continuous Integration with Jenkins

### Pipeline Stages:

```
+------------------+------------------+------------------+------------------+------------------+
| Code & Commit    | Build & Config   | Scan & Test      | Release          | Deploy           |
+------------------+------------------+------------------+------------------+------------------+
| VS, VSCode       | Maven, Gradle    | SonarQube,       | uDeploy,         | AWS, Docker      |
| Eclipse IDE      | Docker, CHEF     | Selenium,        | Serena,          | Azure, VMware    |
| Git, GitHub      | Puppet, Ansible  | Cucumber,        | MidVision,       | OpenStack        |
| Stash, Perforce  | VS               | JUnit            | XL Release       | WebSphere        |
+------------------+------------------+------------------+------------------+------------------+
```

---

## Continuous Deployment with Jenkins

```
Code Terminal --> Storage --> Quality Assurance --> Product Testing
                                                           |
                                                           v
                                                        Products
```

---

## Continuous Delivery

1. Code changes are prepared to be released
2. Frequent releases
3. Compilation of each deployment phase

### Benefits:
1. Continuously releasing the code, changing it, and testing each env
2. Frequent releases
3. Compilation of each deployment phase
4. Faster responses to defects/bugs
5. Automation of entire process
6. More stable, reliable & maintainable CI/CD pipeline
7. Org that requires release of new features on a frequent / daily / hourly basis requires manual approval for coordination
8. The process ensures cross-team coordination

---

## CI/CD Flow Diagram

```
Build --> Test --> Merge --> Automatic Release to Repository --> Automatic Deploy to Production
  |                                     |                                  |
  v                                     v                                  v
Continuous                         Continuous                         Continuous
Integration                         Delivery                          Deployment
```

---

## Traditional Workflow vs Modern

### Traditional Workflow:
```
                    Shared Repo
                        |
Code --> Commit --> VCS --> Create Build
                               |
                        +------+------+
                        |             |
Developer            QAT            SIT
  |               (Testing)       (Testing)
  |                                  |
  +---------> Reports & Test Cases <-+
                        |
                  Deployment
                        |
                  +-----+------+
                  |            |
               UAT/E2E       PITE
                  |
            Product Support
```

---

## Problems with Traditional Approach:
1. Time-consuming
2. Unproductive
3. Changes are costly
4. Lack of transparency
5. Management bottleneck

---

## Modern Development Philosophy

### Agile:
- Emphasizes **adaptive planning** & **evolutionary development**
- "Scrums" — where all team members report progress & plan their next steps
- Work is planned & completed in "Sprints" with frequent feedback

### DevOps:
- Extends the Agile philosophy into operations
- Implements automation monitoring in the development cycle
- Feedback at all steps in the development cycle

---

## Why CI/CD?

1. Detect bugs & problems in the **early stages** of development
2. Saves cost & efforts
3. Faster release to production between systems
4. Automated testing improves quality

---

## Jenkins Workflow

```
Developer
    |
    v
Code Commit
    |
    v
  Git Merge
    |
    +---> Build --> Test --> Scan --> Deploy
    |       |                           |
    |  Continuous                 Continuous
    | Integration                  Delivery
    |
    v
Continuous Feedback & Monitoring
```

### Jenkins Full Pipeline:
```
Build --> Test --> Scan --> Hosted --> Dev --> Val --> Prod
                                  [Continuous Delivery/Deployment]
```
---

## Continuous Delivery vs Continuous Deployment

```
+----------------------------+----------------------------------+----------------------------------+  
| Aspect                     | Continuous Delivery              | Continuous Deployment            |  
+----------------------------+----------------------------------+----------------------------------+  
| Definition                 | Code is always in a deployable   | Every change that passes tests   |    
|                            | state; release is manual         | is deployed to production        |  
|                            |                                  | automatically                    |  
+----------------------------+----------------------------------+----------------------------------+  
| Deployment to Production   | Manual approval required         | Fully automated, no manual       |  
|                            |                                  | intervention                     |  
+----------------------------+----------------------------------+----------------------------------+  
| Release Frequency          | On-demand (team decides when)    | Every passing commit             |  
+----------------------------+----------------------------------+----------------------------------+  
| Human Involvement          | Dev team approves each release   | No human needed after pipeline   |  
|                            |                                  | is set up                        |  
+----------------------------+----------------------------------+----------------------------------+    
| Risk Level                 | Lower — humans review before     | Higher — mistakes reach users    |  
|                            | release                          | faster                           |  
+----------------------------+----------------------------------+----------------------------------+  
| Speed                      | Slower (waiting for approval)    | Fastest possible release cycle   |  
+----------------------------+----------------------------------+----------------------------------+  
| Best For                   | Regulated industries (banking,   | SaaS products, web apps with     |  
|                            | healthcare) needing sign-off     | fast iteration needs             |  
+----------------------------+----------------------------------+----------------------------------+  
| Test Automation Required   | Yes, but manual gate exists      | Yes, must be comprehensive       |  
+----------------------------+----------------------------------+----------------------------------+  
| Rollback                   | Easier — less frequent releases  | Must be automated & fast         |  
+----------------------------+----------------------------------+----------------------------------+  
```

### Pipeline Comparison:

**Continuous Delivery:**
```
Code --> Build --> Test --> Staging --> [MANUAL APPROVAL] --> Production
                                              ^
                                         Team decides
                                         when to release
```

**Continuous Deployment:**
```
Code --> Build --> Test --> Staging --> Production  (fully automatic)
                               |
                         If all tests pass,
                         deploy happens with
                         ZERO manual steps
```

### Key Difference in One Line:
> **Delivery** = *Can* deploy anytime (human clicks the button)  
> **Deployment** = *Does* deploy every time (no button needed)

---




