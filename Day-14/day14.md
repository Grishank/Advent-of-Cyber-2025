# 🎄 Advent of Cyber 2025 — Day 14  
<img src="./images/day14-banner.png" width="900"/>

**Title:** Containers - DoorDasher's Demise  
**Date Completed:** Dec 2025  
**Difficulty:** Medium–Hard  
**Category:** Containers, Docker, Privilege Escalation  
**Room Link:** [Containers - DoorDasher's Demise](https://tryhackme.com/room/container-security-aoc2025-z0x3v6n9m2)  
**Status:** ✔ Completed  

---

## 🧭 Overview  
As the sun rose over Wareville, chaos followed once again.  
DoorDasher, the local food delivery service loved by TBFC employees, had been hijacked by **King Malhare** and rebranded as **Hopperoo**.

Reports flooded in as customers discovered something horrifying in their meals — strands of **Santa’s beard** disguised as noodles.  
With public outrage mounting and health authorities panicking, the SOC team raced to restore the service.

A recovery script was ready — but the engineer was locked out.  
Fortunately, the SOC team still had access via a **monitoring pod container**.

**Mission:**  
Escape the container, escalate privileges, restore DoorDasher, and save the day.

---

## 🎯 Learning Objectives

- Understand how **containers and Docker** work  
- Learn about **Docker images, layers, and container engines**  
- Explore **Docker runtime internals** (daemon, sockets, API)  
- Perform **container escape & privilege escalation**  
- Restore a compromised production service  

---

## 🧠 What Are Containers?

Modern applications face several challenges:

- Installation issues across environments  
- Troubleshooting environment-specific bugs  
- Dependency conflicts between applications  

**Containerisation** solves this by packaging an application and all its dependencies into an isolated unit called a **container**.

Benefits:
- Isolation  
- Portability  
- Lightweight execution  
- Fast startup  

---

## 🆚 Containers vs Virtual Machines

Virtual Machines:
- Run on a hypervisor  
- Include a full guest OS  
- Heavier but fully isolated  

Containers:
- Share the host OS kernel  
- Isolate applications only  
- Lightweight and fast  
- Ideal for microservices  

VMs are best for running different operating systems, while containers excel at scalable, portable services.

---

## 📈 Applications at Scale (Microservices)

Modern applications are increasingly built using **microservices** instead of monoliths.

Advantages:
- Individual components can scale independently  
- Fault isolation  
- Faster deployment cycles  

Containers are the perfect fit for microservices due to their lightweight nature and rapid scalability.

---

## 🐳 Docker Overview

Docker is an open-source **container engine** that builds, runs, and manages containers.

Key features:
- Uses Dockerfiles to define environments  
- Leverages OS kernel features (namespaces, cgroups)  
- Ensures consistent deployments across systems  

Docker is the container engine used at **DoorDasher**.

---

## 🚨 Container Escape & Docker Sockets

A **container escape** occurs when code running inside a container gains access to the host or other containers.

Docker uses a **client-server architecture**:
- Docker CLI → Client  
- Docker daemon → Server  
- Communication via **Unix sockets**

If a container has access to the Docker socket, it can:
- Interact with the Docker API  
- Control other containers  
- Escalate privileges  

---

## 🧪 Challenge Walkthrough

### Step 1 — List Running Containers
- docker ps

### Step 2 — Access the Uptime Checker Container
- docker exec -it uptime-checker sh


Check Docker socket access:
- ls -la /var/run/docker.sock

Docker socket access confirms potential for container escape.

### Step 3 — Verify Docker Access from Inside Container
- docker ps

Docker commands working inside the container confirms access to the Docker API.

### Step 4 — Access the Privileged Deployer Container
- docker exec -it deployer bash


Check user:
- whoami

Explore the container and locate the recovery script.

### Step 5 — Restore DoorDasher
- sudo /recovery_script.sh

Refresh the site:
- http://10.48.138.92:5001

DoorDasher is restored 🎉

### Step 6 — Retrieve the Flag
cat /flag.txt

---

## 🏁 Final Answers / Flags

What command lists running Docker containers?

- docker ps


What file defines instructions for building a Docker image?

- Dockerfile


Flag:

- THM{DOCKER_ESCAPE_SUCCESS}


Bonus — Deployer Password:

- DeployMaster2025!

## 🎯 Learning Objectives Achieved

- Understood container architecture

- Learned Docker runtime internals

- Identified Docker socket abuse

- Performed container escape

- Escalated privileges successfully

- Restored a compromised service

### 📘 What I Learned Today

- “A container is only as secure as the permissions it’s given.”

### 🔜 Next Step
- Proceed to Day 15 of Advent of Cyber 2025.
