# Jenkins Master-Agent Architecture

- In small projects, Jenkins can run everything on a single machine.

- But in large organizations:

   i. Hundreds of builds run daily  
   ii. Multiple teams use Jenkins  
   iii. Different operating systems are required  
   iv. Different testing environments are needed  

- Therefore Jenkins uses a Master-Agent Architecture.

- Master-Agent Architecture is a distributed build system where:

   i. Master controls everything  
   ii. Agents execute jobs

- This distributes workload across multiple machines.
---
## Architecture Diagram  
```
                    Jenkins Master  
                           |  
        --------------------------------------  
        |                  |                |  
        v                  v                v
     Agent 1            Agent 2          Agent3  
      Build              Test            Deploy
```

---
## Working Process
***Step 1:***
 Developer commits code.
```
Developer
    |
    v
Git Repository  
```
***Step 2:***
Jenkins Master receives trigger.
```
GitHub Webhook
        |
        v
Jenkins Master
```
***Step 3:***

Master decides:

- Which node should execute
- Required resources
- Build priority

***Step 4:*** Master assigns task.
```
Master
   |
   +----> Agent
```
***Step 5:***

Agent performs:

- Build
- Testing
- Deployment

***Step 6:*** Results returned to Master.
```
Agent
   |
   v
Master
```
---
## Why Use Master-Agent Architecture?

- ### Without Agents:
```
Master
  |
Build
Test
Deploy
Everything on One Machine
```

***Problems:***
```
- Slow builds
- Resource exhaustion
- Poor scalability
```
- ### With Agents:
```
Master
 |
 +---- Agent 1
 |
 +---- Agent 2
 |
 +---- Agent 3
```
Benefits:
```
Load balancing
Faster execution
Parallel jobs
```
---
## Types of Jenkins Architecture
### Type 1: Single Master Multi-Agent
Most common architecture.

- ***Diagram***  
```
                    Master
                       |
        --------------------------------
        |              |              |
        v              v              v
     Agent1         Agent2         Agent3
```
- ***Example***
```
Master

Agent1 → Linux Build

Agent2 → Windows Testing

Agent3 → Deployment
```
- ***Use Cases:*** Small and Medium Organizations

  Examples:

    Startups  
Product Companies  
Mid-size IT firms  


- ***Advantages***  

   Easy Management  : Only one master to maintain.

  Lower Cost : Less infrastructure required.

  Centralized Control : Everything managed from one dashboard.

- ***Limitation***

   Single Point of Failure
```
Master Down
      ↓
All Agents Stop
```
---
### Type 2: Multi-Master Multi-Agent

- Used in large enterprises.

- ***Diagram***
```
             Master A
         (Retail Banking)
          /      |      \
         /       |       \
     Agent1  Agent2  Agent3


             Master B
         (Capital Banking)
          /      |      \
         /       |       \
     Agent1  Agent2  Agent3
```
- ***Example***

- Banking Organization: 

   Master A Handles: Retail Banking Applications  
   Master B Handles: Capital Banking Applications


- ***Advantages***  

   Better Isolation: Teams work independently.

   Higher Availability: One master failure doesn't impact others.

   Better Scalability: Each department gets dedicated infrastructure.
---
## Benefits of Master-Agent Architecture
***1. Scalability:*** Additional agents can be added anytime.

Example:
```
Today

Master
 |
 +--- Agent1
 +--- Agent2


Tomorrow

Master
 |
 +--- Agent1
 +--- Agent2
 +--- Agent3
 +--- Agent4
 +--- Agent5
```
- No redesign required.

***2. Security:*** Agents execute jobs on separate machines.

- Sensitive data remains protected.
```
Master
    |
Restricted Access

Agent
    |
Build Execution
```
- If Agent is compromised, Master remains protected.

***3. Specialized Nodes:***
Different agents can have different environments.

Example
```
Agent 1
Ubuntu
Java 17

Agent 2
Windows
.NET

Agent 3
Docker
Kubernetes
```
This allows:

Multi-platform testing  
Cross-platform builds  
Environment-specific deployments  

***4. Performance Improvement:*** Workload distributed across machines.

Without Agents
```
Master

Build 1
Build 2
Build 3
Build 4

Executed Sequentially
```
With Agents
```
Master
  |
  +--- Agent1 -> Build 1
  |
  +--- Agent2 -> Build 2
  |
  +--- Agent3 -> Build 3
  |
  +--- Agent4 -> Build 4

Executed in Parallel.
```
Result:

   Faster builds  
   Better resource utilization  
   Reduced waiting time  

---
## Jenkins Components
Component Diagram
```
Master
   |
   | (TCP/IP)
   |
 Agent
   |
Executors
```
### A. Master (Controller)
Master is the Jenkins server responsible for:


l-> Job Scheduling  
l-> Pipeline Management  
l-> Security  
l-> Monitoring  
l-> Configuration   


- ***Responsibilities*** 

i. Job Scheduling   
Determines:
```
When?
Where?
How?
```
a build should run.

ii. User Management Handles:
```
Authentication
Authorization
RBAC
```
iii. Plugin Management

Controls Jenkins plugins.

Examples:
```
Git Plugin
Docker Plugin
SonarQube Plugin
```
iv. Build Monitoring

Tracks:
```
Running Builds  
Failed Builds  
Queue Status  
```


### B. Node

A Node is any machine capable of running Jenkins jobs.

- ***Can be:***

   Linux Server  
   Windows Server   
   Cloud VM  

- ***Examples***
```
Node 1 → Ubuntu

Node 2 → Windows

Node 3 → AWS EC2
```
### C. Agent
- Agent is software installed on a Node.

- It receives instructions from Master.

- ***Workflow***
```
Master
   |
Assign Job
   |
Agent
   |
Execute Job
```
- ***Responsibilities***
  
Build execution  
Test execution    
Deployment execution  


### D. Executor

- Executor is a worker thread inside an Agent.

- It performs actual build execution.

- ***Example***

Agent contains:
```
Agent

Executor 1

Executor 2

Executor 3

Executor 4
````
- ***Function***
```
Number of Executors determines How many jobs can run simultaneously?
```
Example:
```
Executors = 4

Maximum Parallel Jobs = 4
```
---
## Complete Architecture
```
                    Jenkins Master
                           |
                    Job Scheduling
                           |
          -----------------------------------
          |                |                |
          v                v                v
       Agent1          Agent2          Agent3

    Executor1       Executor1       Executor1
    Executor2       Executor2       Executor2
    Executor3
    Executor4

```
