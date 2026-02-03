# DevOps Intern Final Assessment

**Name:** Muhammad Uzair
**Date:** 03 February 2026

---

## Overview

This repository contains my final assessment project for the DevOps internship. The goal was to create a **small but realistic DevOps workflow** using tools and concepts I’ve learned, including Git, Linux scripting, Docker, CI/CD, Nomad, and basic monitoring.

I approached this project as if I were setting up a mini DevOps pipeline for a real application, documenting each step along the way.

---

## Repository Structure

```
Final-Assessment/
│
├── hello.py
├── README.md
├── Dockerfile
├── scripts/
│   └── sysinfo.sh
├── .github/
│   └── workflows/
│       └── ci.yml
├── nomad/
│   └── hello.nomad
├── monitoring/
│   └── loki_setup.txt
```

---

## 1. Git & GitHub Setup

I started by creating a public GitHub repository and initializing Git locally. I added a simple Python script `hello.py` to verify the repo setup.

### hello.py

```python
print("Hello, DevOps!")
```

This was my first step to ensure Git tracking and basic script functionality.

---

## 2. Linux & Scripting Basics

Next, I created a small shell script to gather system information. Since I’m working on Windows, I included a note about Linux execution.

### File: `scripts/sysinfo.sh`

```bash
#!/bin/bash

echo "Current User:"
whoami

echo "Current Date:"
date

echo "Disk Usage:"
df -h
```

> **Note:** On Linux, you would run `chmod +x scripts/sysinfo.sh` to make it executable.

This step helped me practice basic Linux commands and scripting logic.

---

## 3. Docker Basics

I containerized the Python script using Docker to understand container workflows.

### Dockerfile

```Dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY hello.py .
CMD ["python", "hello.py"]
```

### Commands to Build & Run

```bash
docker build -t hello-devops .
docker run hello-devops
```

**Output:** `Hello, DevOps!`

This was a practical exercise to see how Docker isolates environments and runs applications.

---

## 4. CI/CD with GitHub Actions

I created a GitHub Actions workflow to run the Python script automatically whenever changes are pushed.

### File: `.github/workflows/ci.yml`

```yaml
name: CI Pipeline

on: [push]

jobs:
  run-hello:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Hello Script
        run: python hello.py
```

This ensures continuous validation of the project without manual intervention.

---

## 5. Job Deployment with Nomad

I wrote a Nomad job file to deploy the Docker container as a service with minimal resources.

### File: `nomad/hello.nomad`

```hcl
job "hello-devops" {
  datacenters = ["dc1"]
  type = "service"

  group "hello-group" {
    task "hello-task" {
      driver = "docker"

      config {
        image = "hello-devops"
      }

      resources {
        cpu    = 100
        memory = 128
      }
    }
  }
}
```

### Run Command

```bash
nomad job run nomad/hello.nomad
```

This step gave me hands-on experience with job orchestration and resource allocation.

---

## 6. Monitoring with Grafana Loki

I documented a basic setup for Loki monitoring to capture logs from containers.

### File: `monitoring/loki_setup.txt`

* Started Loki using Docker.
* Checked container logs with `docker logs <container_id>`.
* Loki accessible at `http://localhost:3100`.

This taught me how to forward and view logs from running services.

---

## Optional Enhancements

For extra practice, I considered adding:

* MLflow experiment tracking.
* Running the Docker/Nomad setup inside a VM.

This shows an understanding of advanced deployment and monitoring strategies, though it wasn’t implemented for this assessment.

---

## What I Learned

* How to manage code with Git and GitHub.
* Linux scripting fundamentals and system commands.
* Containerizing applications with Docker.
* Setting up CI/CD pipelines using GitHub Actions.
* Deploying services with Nomad.
* Basic log monitoring with Grafana Loki.

Overall, this project helped me think like a DevOps engineer, planning, building, and documenting a workflow end-to-end.

---

## Conclusion

This assessment reflects my ability to implement practical DevOps solutions while documenting each step clearly. It also demonstrates an understanding of modern DevOps tools and best practices.

