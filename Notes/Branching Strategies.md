# Branching Strategies

There are two commonly used enterprise branching strategies:

1. GitFlow-Based CI/CD
2. Trunk-Based Development (TBD)

---

## A. GitFlow-Based CI/CD

## Goal

- Strong environment isolation
- Controlled release process
- Higher stability
- Better suited for large enterprise applications

---

## Branch Structure

```text
main
 │
 ├── stage
 │
 ├── dev
 │
 └── feature/*
```

---

## Workflow

### Step 1: Create Feature Branch

```text
main
 └── feature/login-feature
```

Developer:

- Creates feature branch
- Commits code
- Pushes changes

---

### Step 2: Open PR to Dev

```text
feature --> dev
```

Rules:

- Dev branch is protected
- Direct commits are blocked
- Code review required
- CI checks must pass

---

### Step 3: PR CI Pipeline

```text
Checkout
   ↓
Build
   ↓
Unit Tests
   ↓
Integration Tests
   ↓
Lint
   ↓
Static Analysis
```

---

### Step 4: Status Gate

```text
Green  → Merge Allowed
Red    → Merge Blocked
```

---

### Step 5: Merge into Dev

```text
feature --> dev
```

After merge:

- Dev contains validated code
- Ready for deployment

---

### Step 6: Auto Deploy to Dev

```text
Dev Branch
     ↓
Build Artifact
     ↓
Deploy to Dev
     ↓
Smoke Test
     ↓
Health Check
```

If deployment fails:

```text
Rollback
   ↓
Fix
   ↓
New PR
```

---

# Promotion Flow (Dev → Stage)

### Step 1: Promotion PR

```text
dev --> stage
```

Purpose:

- Promote the exact tested version
- No new code changes

---

### Step 2: Deploy to Stage

```text
Same Artifact
      ↓
Stage Configuration
      ↓
Deploy
```

No rebuild is performed.

---

### Step 3: Validation

Run:

- Functional Tests
- Regression Tests
- UAT Testing
- Performance Checks

---

### Step 4: Decision

```text
Green → Promote
Red   → Fix & Re-promote
```

---

# Production Deployment

## Deploy Same Artifact

### Golden Rule

> Build Once, Deploy Everywhere

Never rebuild for production.

---

## Canary Deployment

```text
10%
 ↓
20%
 ↓
50%
 ↓
100%
```

Monitor at each stage.

---

## Blue-Green Deployment

```text
Blue Environment  → Current Production

Green Environment → New Version

Traffic Switch
        ↓
Green Becomes Production
```

---

## Complete GitFlow Diagram

```text
main
 │
 ├── stage
 │     ↑
 │     │
 ├── dev
 │     ↑
 │     │
 └── feature/*
```

---

# B. Trunk-Based Development (TBD)

## Goal

- Fast integration
- Continuous delivery
- Small changes
- Frequent deployments

---

## Branch Structure

```text
main
 │
 └── feature/small-change
```

Feature branches are short-lived.

---

## Core Principles

### Small Changes

- Few files
- Few commits
- Easy review

### Frequent Merges

- Merge daily if possible

### Main Always Releasable

At any time:

```text
main = production ready
```

---

## Workflow

### Step 1: Create Feature Branch

```text
main
 └── feature/payment-fix
```

Developer:

- Develops feature
- Commits code
- Pushes changes

---

### Step 2: Open PR to Main

```text
feature --> main
```

Protected branch rules:

- Review required
- CI checks required
- Direct push blocked

---

### Step 3: PR CI

```text
Checkout
   ↓
Build
   ↓
Unit Tests
   ↓
Lint
   ↓
Static Analysis
```

---

### Step 4: Merge Decision

```text
Green → Merge
Red   → Fix
```

---

### Step 5: Merge to Main

```text
feature --> main
```

Main now points to a known-good commit.

---

## Post-Merge Build

Build only once.

```text
Main
  ↓
Build Artifact
  ↓
Push Docker Image
  ↓
Store Digest
  ↓
Publish Manifest
```

---

## Continuous Delivery Flow

### Dev

```text
Deploy Same Digest
      ↓
Smoke Tests
      ↓
Health Checks
```

### Stage

```text
Promote Same Digest
        ↓
Run Validation Tests
```

### Production

```text
Promote Same Digest
        ↓
Approval (Optional)
        ↓
Canary / Blue-Green
```

---

## Complete Trunk-Based Diagram

```text
main
 │
 └── feature/*
        │
        ▼
      PR
        │
        ▼
      main
        │
        ▼
    Build Once
        │
        ▼
 Deploy Everywhere
```

---

# GitFlow vs Trunk-Based Development

| Parameter | GitFlow | Trunk-Based |  
|------------|----------|------------|  
| Branches | feature → dev → stage → prod | feature → main |  
| Complexity | High | Low |  
| Release Speed | Slower | Faster |    
| Merge Frequency | Lower | Higher |  
| Risk Handling | Environment Isolation | Small Frequent Changes |  
| Deployment Style | Promotion Through Branches | Promotion Through Artifact Digest |  
| Suitable For | Large Enterprises | Cloud Native Teams |  
| Feedback Cycle | Longer | Shorter |  
| Delivery | Controlled | Continuous |  

---

# Summary

## GitFlow

- Multiple long-lived branches
- Strong environment separation
- Better control over releases
- Suitable for large enterprise projects

## Trunk-Based Development

- Single main branch
- Small and frequent changes
- Faster releases
- Ideal for cloud-native and DevOps teams
- Supports continuous integration and continuous delivery
