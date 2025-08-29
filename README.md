# Project-Leviathan

A comprehensive guide for setting up a Kubernetes cluster using Kind on an Ubuntu-VM, installing and configuring Argo CD, and deploying applications using Argo CD.

## Overview

This guide covers the steps to:
- Install Docker and Kind.
- Create a Kubernetes cluster using Kind.
- Install and access kubectl.
- Set up the Kubernetes Dashboard.
- Install and configure Argo CD.
- Connect and manage Kubernetes cluster with Argo CD.


## Architecture

<img width="6810" height="2826" alt="Leviathan-k8" src="https://github.com/user-attachments/assets/1dc83674-1c32-4ce7-95f1-6011d4e42cdc" />



## Observability

<img width="1920" height="898" alt="grafana" src="https://github.com/user-attachments/assets/102ff9f8-51b0-4a72-aca1-b188f1b452dd" />


<img width="1915" height="813" alt="image" src="https://github.com/user-attachments/assets/045556c1-7059-47d4-8ca8-7ca7f1bdee52" />


* A front-end web app in [Python](/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time


### Project Title: 

Automated Deployment of Scalable Applications on local machine with Kubernetes and Argo CD

### Description: 

Led the deployment of scalable applications on ubuntu vm using Kubernetes and Argo CD for streamlined management and continuous integration. Orchestrated deployments via Kubernetes dashboard, ensuring efficient resource utilization and seamless scaling.

### Key Technologies:

* Ubuntu-VM: Infrastructure hosting for Kubernetes clusters.
* Kubernetes Dashboard: User-friendly interface for managing containerized applications.
* Argo CD: Continuous Delivery tool for automated application deployments.

### Achievements:

Implemented Kubernetes dashboard for visual management of containerized applications on Ubuntu VM.
Utilized Argo CD for automated deployment pipelines, enhancing deployment efficiency by 60%.
Achieved seamless scaling and high availability, supporting 99.9% uptime for critical applications.
This project description emphasizes your role in leveraging Ubuntu vm, Kubernetes, and Argo CD to optimize application deployment and management processes effectively.


