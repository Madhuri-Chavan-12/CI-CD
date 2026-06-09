# Jenkins Master-Slave Architecture



Jenkins is designed to support distributed builds through a Master-Slave (Controller-Agent) architecture.

Instead of executing every build on a single machine, Jenkins distributes workloads across multiple nodes, improving scalability, performance, and reliability.

In modern Jenkins versions:

* Master = Controller
* Slave = Agent

However, many organizations still use the older terminology.

---

# Why Do We Need Distributed Builds?

Imagine a company with:

* Multiple projects
* Hundreds of developers
* Thousands of builds every day

Running all builds on a single Jenkins server would create:

* CPU bottlenecks
* Memory bottlenecks
* Slow build execution
* Single point of failure

To solve this problem Jenkins distributes builds across multiple machines.

---

# Architecture Overview

## 1. Single Master Multi Slave

```

                +----------------+
                | Jenkins Master |
                +--------+-------+
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
   +-----------+    +-----------+    +-----------+
   |  Agent 1  |    |  Agent 2  |    |  Agent 3  |
   +-----------+    +-----------+    +-----------+
```

The master schedules jobs and agents execute them.

---

## 2. Multi Master Multi Slave

Large enterprises often maintain multiple Jenkins installations.

Example:

```
┌─────────────────────────┐
│ Retail Banking Master   │
└───────────┬─────────────┘
            │
     ┌──────┼──────┐
     │      │      │
     ▼      ▼      ▼
┌────────┐ ┌────────┐ ┌────────┐
│Agent 1 │ │Agent 2 │ │Agent 3 │
└────────┘ └────────┘ └────────┘
----------------------------------------

┌─────────────────────────┐
│ Capital Banking Master  │
└───────────┬─────────────┘
            │
     ┌──────┼──────┐
     │      │      │
     ▼      ▼      ▼
┌────────┐ ┌────────┐ ┌────────┐
│Agent 1 │ │Agent 2 │ │Agent 3 │
└────────┘ └────────┘ └────────┘
```

Each business unit manages its own Jenkins infrastructure.

---

# Jenkins Components

## 1. Master (Controller)

The controller is the brain of Jenkins.

Responsibilities:

* Job scheduling
* Pipeline orchestration
* User management
* RBAC management
* Plugin management
* Agent management
* Build history management

The controller should not be overloaded with build execution tasks.

---

## 2. Node

A node is any machine connected to Jenkins.

Examples:

* Linux VM
* Windows Server
* Cloud VM
* EC2 Instance
* Physical Machine

Nodes provide resources required for builds.

---

## 3. Agent

Agents execute the actual build tasks.

Responsibilities:

* Receive work from controller
* Execute pipeline stages
* Return build results

Agents are lightweight Jenkins runtimes installed on nodes.

---

## 4. Executor

An executor is a worker thread available on a node.

Example:

Node A

Executors = 4

```text
Executor 1 -> Build A
Executor 2 -> Build B
Executor 3 -> Build C
Executor 4 -> Build D
```

All builds can run simultaneously.

The number of executors determines how many concurrent jobs a node can execute.

---

# Build Execution Flow

```
┌─────────────┐
│  Developer  │
└──────┬──────┘
       │ Trigger Build
       ▼
┌─────────────────┐
│ Jenkins Master  │
└──────┬──────────┘
       │ Assign Job
       ▼
┌─────────────────┐
│ Jenkins Agent   │
└──────┬──────────┘
       │
       │ Execute Build
       ▼
┌─────────────────┐
│ Build Process   │
└──────┬──────────┘
       │ Return Results
       ▼
┌─────────────────┐
│ Jenkins Master  │
└──────┬──────────┘
       │ Build Status
       ▼
┌─────────────┐
│  Developer  │
└─────────────┘
```

---

# Benefits of Master-Slave Architecture

## Scalability

Additional agents can be added whenever required.

Benefits:

* Horizontal scaling
* Better resource utilization
* Increased build capacity

---

## Security

Jobs run on isolated machines.

Benefits:

* Reduced attack surface
* Sensitive controller data remains protected
* Environment isolation

---

## Specialized Nodes

Different agents can support different technologies.

Example:

| Agent         | Purpose           |  
| ------------- | ----------------- |  
| Linux Agent   | Java Applications |  
| Windows Agent | .NET Applications |  
| Mac Agent     | iOS Builds        |  

---

## Performance

Multiple builds can run simultaneously.

Benefits:

* Reduced queue time
* Faster feedback
* Better developer productivity

---

# Real World Example

A banking application contains:

* Retail Banking
* Capital Banking
* Payments
* Loans

Instead of using one Jenkins server:

* Retail Banking uses its own master.
* Capital Banking uses its own master.
* Each master manages its own agents.

This improves:

* Isolation
* Security
* Scalability
