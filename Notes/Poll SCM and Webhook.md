## Jenkins Webhooks

A **webhook** is an HTTP callback triggered by an event. When code is pushed to GitHub/GitLab/Bitbucket, the VCS sends an HTTP POST request to Jenkins — Jenkins reacts immediately.

### How Webhook Works:
```
Developer                  GitHub / GitLab              Jenkins
    |                           |                          |
    |--- git push ------------>>|                          |
    |                           |--- HTTP POST ---------->>|
    |                           |   (webhook payload)      |
    |                           |                          |--- Trigger Build
    |                           |                          |--- Run Pipeline
    |                           |                          |--- Report Status
```

### Webhook Setup Steps:
```
1. Jenkins side:
   Dashboard --> Job --> Configure --> Build Triggers
   --> [x] GitHub hook trigger for GITScm polling

2. GitHub side:
   Repo --> Settings --> Webhooks --> Add Webhook
   --> Payload URL : http://<jenkins-url>/github-webhook/
   --> Content-Type: application/json
   --> Events     : Just the push event (or PR, etc.)
   --> [x] Active --> Add Webhook
```

### Jenkinsfile trigger syntax:
```groovy
pipeline {
    triggers {
        githubPush()   // webhook-based trigger
    }
    ...
}
```

---

## Poll SCM

Jenkins itself **polls** (checks) the repository at a scheduled interval using cron syntax. If changes are found, it triggers a build.

### How Poll SCM Works:
```
Jenkins                    GitHub / GitLab
    |                           |
    |--- "Any changes?" ----->>|   (every N minutes)
    |                           |
    |<<-- "Yes / No" ----------|
    |                           |
    (if Yes) --> Trigger Build
    (if No)  --> Do nothing, wait for next poll
```

### Poll SCM Setup:
```
Dashboard --> Job --> Configure --> Build Triggers
--> [x] Poll SCM
--> Schedule:  H/15 * * * *   (every 15 minutes)
               H/5  * * * *   (every 5 minutes)
               H * * * *      (every hour)
```

> **Note on `H`:** Jenkins-specific symbol — adds a hash-based offset so all jobs don't poll at the exact same time. Prevents server overload.

### Jenkinsfile trigger syntax:
```groovy
pipeline {
    triggers {
        pollSCM('H/15 * * * *')   // poll every 15 min
    }
    ...
}
```

---

## Webhook vs Poll SCM — Comparison

```
+------------------------+---------------------------+-----------------------------+
| Aspect                 | Webhook                   | Poll SCM                    |
+------------------------+---------------------------+-----------------------------+
| Trigger Type           | Event-driven (push-based) | Schedule-based (pull-based) |
+------------------------+---------------------------+-----------------------------+
| Who initiates?         | GitHub/GitLab notifies    | Jenkins asks the repo       |
|                        | Jenkins                   | periodically                |
+------------------------+---------------------------+-----------------------------+
| Speed                  | Instant (real-time)       | Delayed (up to poll         |
|                        |                           | interval, e.g. 15 min)      |
+------------------------+---------------------------+-----------------------------+
| Resource Usage         | Very efficient — fires    | Wasteful — Jenkins makes    |
|                        | only on actual events     | repeated Git requests even  |
|                        |                           | if nothing changed          |
+------------------------+---------------------------+-----------------------------+
| Network Requirement    | Jenkins must be publicly  | Jenkins can be behind       |
|                        | reachable (open port)     | firewall; no inbound needed |
+------------------------+---------------------------+-----------------------------+
| Setup Complexity       | Slightly more setup       | Simpler to configure        |
|                        | (webhook on VCS side too) |                             |
+------------------------+---------------------------+-----------------------------+
| Recommended For        | Production environments,  | Jenkins behind firewall,    |
|                        | most modern CI/CD setups  | restricted network, or when |
|                        |                           | VCS doesn't support webhook |
+------------------------+---------------------------+-----------------------------+
| Scalability            | Scales well — no polling  | Poor at scale — 50 jobs x   |
|                        | overhead                  | 5 min = 600 Git req/hour    |
+------------------------+---------------------------+-----------------------------+
| Missed Events          | Rare (if Jenkins is down  | Can miss nothing — always   |
|                        | during push, event lost)  | checks on schedule          |
+------------------------+---------------------------+-----------------------------+
| Best Practice          | YES — preferred method    | Fallback only               |
+------------------------+---------------------------+-----------------------------+
```

### Decision Flowchart:
```
Is Jenkins publicly reachable?
        |
       YES --> Use WEBHOOK  (faster, efficient, production-grade)
        |
       NO
        |
Does VCS support webhooks?
        |
       NO --> Use POLL SCM  (fallback option)
        |
       YES
        |
Can you expose Jenkins via reverse proxy / ngrok?
        |
       YES --> Use WEBHOOK
        |
       NO  --> Use POLL SCM
```

### Also: Build Periodically (3rd trigger type)
```
+------------------------+---------------------------+-----------------------------+
| Build Periodically     | Runs on cron schedule     | Does NOT check for changes  |
|                        | regardless of changes     | — always builds             |
+------------------------+---------------------------+-----------------------------+
```
> **Poll SCM** vs **Build Periodically**: Poll SCM only builds if something changed. Build Periodically builds every time, even if no code changed. Poll SCM is better of the two — but Webhook beats both.

