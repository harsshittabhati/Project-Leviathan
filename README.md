# Project Leviathan
### An Autonomous, Threat-Informed, Zero Trust Defense Ecosystem

---

## Project Overview

Project Leviathan successfully delivered a comprehensive, zero-trust security ecosystem within the constraints of a single-VM environment. Despite significant resource limitations, the project achieved all core objectives through innovative memory management, orchestrated service deployments, and practical security validation.The entire platform's infrastructure and security policies are managed as code, with Argo CD serving as the single source of truth.

## Architecture
<img width="930" height="619" alt="Leviathan drawio" src="https://github.com/user-attachments/assets/117cd3a6-5806-42e1-ac13-0dd040de4f2e" />

## Observability

<img width="1920" height="898" alt="grafana" src="https://github.com/user-attachments/assets/102ff9f8-51b0-4a72-aca1-b188f1b452dd" />


<img width="1915" height="813" alt="image" src="https://github.com/user-attachments/assets/045556c1-7059-47d4-8ca8-7ca7f1bdee52" />


* A front-end web app in [Python](/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time

## Core Principles

The architecture was designed around four foundational security concepts:

> *Assume Breach*
> Design every component with the assumption that adversaries are already inside the network.

> *Infrastructure is Code*
> The entire state of the platform is defined declaratively, with Git as the single source of truth.

> *Automate Everything*
> Employ a comprehensive automation approach to all operations and incident response procedures.

> *Intelligence Drives Action*
> Transform disparate events into unified intelligence that directly triggers autonomous defensive actions through integrated systems.

---

## Technical Architecture

The platform successfully integrates over 20 services within a 12GB memory budget.

#### Core Infrastructure
* *Orchestration*: Kubernetes via kind (1 control-plane + 2 workers) 
* *Network*: Cilium CNI with eBPF dataplane and micro-segmentation
* *Service Mesh*: Istio with mTLS STRICT enforcement 
* *GitOps*: Argo CD with an app-of-apps pattern 
* *Load Balancing*: MetalLB for LoadBalancer service support 

#### Security Stack
* *Policy Engine*: Kyverno for admission control and supply chain security 
* *Image Verification*: Cosign integration for signed image enforcement 
* *Runtime Security*: Falco for behavioral monitoring and threat detection 
* *Deception Technology*: A custom Python-based honeytoken HTTP service 
* *Chaos Engineering*: Chaos Mesh for resilience testing 
* *Access Control*: Pomerium identity-aware proxy for dashboard access 

#### Intelligence & Automation
* *Secret Management*: HashiCorp Vault in a production-hardened configuration 
* *Event Streaming*: Kafka for real-time security event processing 
* *Graph Database*: Neo4j for asset relationship mapping and attack path analysis 
* *SOAR Platform*: n8n for automated incident response workflows 

---

## Security Validation: Honeytoken Attack Simulation

The ecosystem's defense capabilities were validated through a practical adversary simulation.

* *Implementation*: A Python HTTP server was deployed to expose deceptive endpoints like /sensitive-data and /admin.
* *Attack Method*: An internal pod simulated a compromised workload by using curl to target the honeytoken service's endpoints.
* *Result: **100% of all 15+ unauthorized access attempts were captured* with sub-200ms logging latency, providing complete HTTP logs for forensic analysis.

---

## Resource Management & Orchestration

A primary challenge was deploying the entire stack within a 12GB VM. This was solved using an orchestrated sync-wave deployment strategy.

* *Wave 1*: Core platform services (Cilium, Istio, Argo CD)
* *Wave 2*: Security and defense services (Kyverno, Chaos Mesh, Honeytokens) 
* *Wave 3*: Intelligence and data services (Kafka, Neo4j, Vault, Falco, n8n) 

This approach enabled the full deployment of the ecosystem while maintaining platform stability.

## OKR Achievement Summary

| Objective | Key Result | Status | Notes |
| :--- | :--- | :--- | :--- |
| *Declarative Ecosystem* | GitOps (Argo CD) | *ACHIEVED* | All platform state managed via Argo CD with a complete Git audit trail. |
| | Cilium CNI | *ACHIEVED* | eBPF network policies operational with micro-segmentation. |
| | DR < 15 min | *ADAPTED* | VM snapshot recovery validated (45 min RTO); regional DR documented for future multi-VM deployment. |
| *Zero-Trust Posture* | Cosign + Kyverno | *ACHIEVED* | Supply chain security enforced with unsigned image blocking. |
| | Honeytokens | *ACHIEVED* | Python honeytoken service deployed with 100% detection rate for 15+ access attempts. |
| *Security Intelligence* | Kafka Event Streaming | *ACHIEVED* | Event streaming via Kafka with canonical schema processing is operational. |
| | Neo4j Asset Graph | *ACHIEVED* | Asset inventory and relationship mapping is operational. |

---

## Deployment via GitOps

The entire platform state is managed declaratively. To deploy, point an Argo CD instance to the Git repository.

```yaml
# Example: Argo CD Root Application
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: root
  namespace: argocd
spec:
  project: default
  source:
    repoURL: '[https://github.com/harsshittabhati/Project-Leviathan.git](https://github.com/harsshittabhati/Project-Leviathan.git)'
    path: argocd/apps
    targetRevision: HEAD
  destination:
    server: '[https://kubernetes.default.svc](https://kubernetes.default.svc)'
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
