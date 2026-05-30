# 1. CI → Continuous Integration

* CI/CD is a modern software development practice that automates the process of building, testing and deploying applications.

* Its main goal is to deliver software faster, with fewer bugs and better quality.


* Continuous Integration is a development practice where developers frequently integrate their code into a shared repository.

* Each integration is verified automatically using:

      Build process
      Unit testing
      Code quality checks
      Security scanning

This helps detect bugs and integration issues at an early stage.

### Activities in Continuous Integration   

***1. Develop and Compile***

- Developers write code and push it to Git repository.  
- The CI server automatically:  
      i. Fetches code  
      ii. Compiles source code   
    iii. Creates build artifacts    

***2. Perform Unit Testing***

- After build completion:

    i. Unit tests are executed  
    ii. Code functionality is verified  
   iii. Failed tests stop the pipeline  


***3. Database Integration***

- Application is tested with databases.

Examples:
```
MySQL  
PostgreSQL  
MongoDB  
```


Purpose:
```
Verify database connectivity  
Validate queries  
Check schema compatibility  
```

***4. Functional Testing***

- Tests application functionality from user perspective.


Examples:
```
Login testing  
Registration testing  
API validation  
```
Tools
```
Selenium  
Cypress  
Cucumber  
```

***5. Production Deployment Validation***

- Before deployment:

i. Environment compatibility is checked  
ii. Configuration validation is performed    

***6. Reporting and Analysis***

- CI tools generate reports for:

Build status   
Test results  
Code coverage  
Security findings  

Tools:
```
SonarQube  
Jacoco  
```

### CI Workflow  

```
Developer -> Commit Code -> Git Repository -> Jenkins Trigger -> Build -> Unit Test -> Code Scan -> Artifact Generated 
``` 



### Benefits of Continuous Integration

***i. Early Bug Detection:*** Issues are found immediately after code commit.

***ii. Better Code Quality:***  Automated tests ensure stable code.

***iii. Faster Development:*** Developers receive quick feedback.

***iv. Reduced Integration Problems:*** Small code changes are easier to merge.

***v. Improved Collaboration:*** Multiple developers can work simultaneously.


# 2. CD → Continuous Delivery / Continuous Deployment


- Continuous Deployment aims to reduce the time between:
```
Writing Code
        ↓
Production Deployment
```
- Every successful change automatically reaches production without manual intervention.

### Characteristics
***1. Highly Automated Process:*** Most deployment activities are automated.

Benefits:

``` 
Accuracy  
Consistency    
Speed
```

***2. Scripts Replace Manual Tasks***

Automation scripts perform:  
```
Build  
Testing  
Deployment  
Configuration  
```
Examples:
```
Jenkins  
Shell Scripts  
Ansible  
Terraform  
```
***3. Environment Creation***

- Deployment tools can automatically create infrastructure.

Examples:  
```
AWS EC2  
Kubernetes Cluster  
Docker Containers  
```

### Continuous Deployment Flow
```
Code Commit -> Build -> Test -> Security Scan -> Deploy -> Production
```

### Jenkins Ecosystem
                 
```
1. Code & Commit

VS Code  
Git  
GitHub  
Bitbucket  
------------------------
2. Build & Configure

Maven
Gradle
Docker
Chef
Puppet
Ansible
-------------------------
3. Scan & Test

SonarQube
JUnit
Selenium
Cucumber
------------------------
4. Release

uDeploy
Serena
XL Release
------------------------
5. Deploy

AWS
Azure
VMware
OpenStack
WebSphere`
```

### Continuous Delivery vs Continuous Deployment
 
| Continuous Delivery	| Continuous Deployment |    
| ---------------------| ------------------------|   
| Code is prepared for release	|  Code is automatically released  |   
| Requires manual approval | 	No manual approval  |   
| Frequent releases	|  Continuous releases  |     
| Smaller release packages	| Immediate production updates  |   
| Faster bug response | 	Faster customer delivery  |   
| Suitable for regulated environments	|  Suitable for fully automated environments  |  
| Code -> Build -> Test -> Release ->  Repository -> Manual Approval -> Production |  Code -> Build -> Test -> Release -> Repository -> Automatic Deploy -> Production |  
