---
layout: post
title:  "Docker foundations"
date:   2025-04-14 17:09:25 +0700
categories: docker 
---

# Foundations   
🎯 Goal: Understand what Docker is, why it’s used, and how to run basic containers.
1. What is Docker?
2. Docker vs Virtual Machines
3. Docker Architecture (Daemon, CLI, Images, Containers)
4. Installing Docker (Windows, macOS, Linux)
5. Basic Docker Commands:docker run, docker ps, docker stop, docker rm, docker exec, docker logs

# 🐳 What is Docker?

## 🔍 Overview

**Docker** is an open-source platform designed to automate the deployment, scaling, and management of applications using **containerization**.

A **container** is a lightweight, standalone, and executable software package that includes everything needed to run an application:  
> **code, runtime, system tools, libraries, and settings**.

---

## 🧱 Why Docker?

### ✅ Benefits of Docker:

- **Portability**: Run the same container anywhere (development, staging, production)
- **Consistency**: Eliminates the "it works on my machine" problem
- **Efficiency**: Lightweight compared to virtual machines (shares host OS kernel)
- **Speed**: Start/stop containers in seconds
- **Isolation**: Each container runs independently
- **Scalability**: Easy to replicate and scale containers

---

## 🔧 Key Components of Docker

| Component     | Description |
|---------------|-------------|
| **Docker Engine** | The core service that creates and manages containers |
| **Images**     | Read-only templates used to create containers |
| **Containers** | Running instances of Docker images |
| **Dockerfile** | Script to define how an image is built |
| **Docker Hub** | Public registry to share and pull container images |
| **Docker Compose** | Tool for defining and managing multi-container applications |

---

## 🔄 Docker vs Virtual Machines

| Feature         | Docker (Containers)     | Virtual Machines       |
|------------------|-------------------------|-------------------------|
| Startup Time     | Seconds                 | Minutes                 |
| Resource Usage   | Low (shares host kernel) | High (includes full OS) |
| Portability      | High                    | Medium                  |
| Isolation Level  | Process-level           | Hardware-level          |

---

## 📦 Example Use Case

You can package a **Node.js** application with **Nginx** and **MongoDB** into containers. These containers can be run on any system with Docker installed, ensuring consistency across development, testing, and production environments.

```bash
docker run -d -p 80:80 nginx

