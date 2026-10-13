# Cybersecurity Learning Journal — Day 2
## Virtualization, Containers, Network Ports & Cloud Computing

**Date:** October 12, 2026  
**Platform:** TryHackMe  
**Learning focus:** Computer infrastructure, virtualization, containers, cloud computing, and security responsibilities.

---

## 1. Virtualization

### What is virtualization?

Virtualization is a technology that allows multiple virtual computing environments to operate on a single physical computer.

Each virtual machine (VM) behaves like an independent computer with its own operating system, allocated memory, storage, and virtual hardware.

### Hypervisor

A **hypervisor** is software or firmware that creates and manages virtual machines.

There are two main types:

**Type 1 — Bare-metal hypervisor**
- Runs directly on physical hardware.
- Commonly used in enterprise data centres.
- Examples: VMware ESXi and Microsoft Hyper-V Server.

**Type 2 — Hosted hypervisor**
- Runs on top of an existing operating system.
- Commonly used for development, testing, and home labs.
- Example: Oracle VirtualBox.

### Practical example

My cybersecurity lab uses:

- Host operating system: Windows 11
- Hypervisor: Oracle VirtualBox
- Guest operating system: Ubuntu Linux
- Purpose: Cybersecurity training and testing

### Lab machine

A lab machine is a computer or virtual environment used for learning, experimentation, troubleshooting, and security testing.

A lab may contain an attacker machine, a target machine, or multiple systems connected through a virtual network.

**Security relevance:** Virtualization allows security professionals to practise in controlled environments without needing multiple physical computers.

---

## 2. Containers

### What is a container?

A container is an isolated environment that packages and runs an application together with its required libraries and dependencies.

Unlike virtual machines, containers generally share the host operating system's kernel instead of running a complete guest operating system.

### Containers vs. virtual machines

| Virtual machine | Container |
|---|---|
| Runs a guest operating system | Shares the host kernel |
| Typically requires more resources | Typically uses fewer resources |
| Usually slower to start | Usually faster to start |
| Virtualizes hardware | Isolates application processes |
| Useful for complete operating-system labs | Useful for deploying applications |

### Container image

A **container image** is a packaged, generally read-only template used to create containers.

An image can contain:
- Application code
- Runtime environment
- Libraries
- Dependencies
- Configuration files

**Important distinction:**

- Image = Packaged template
- Container = Instance created from that image

One image can be used to create multiple containers.

### Docker

Docker is a platform for building, distributing, and running containers.

Example:

```bash
docker run nginx
```

This command creates and starts a container using the Nginx image.

Nginx is software commonly used to serve websites and handle HTTP requests.

### Security relevance

Containers introduce security considerations such as:

- Vulnerable or outdated container images
- Excessive container privileges
- Exposed services
- Insecure configurations
- Container escape vulnerabilities

A **container escape** occurs when an attacker breaks out of the intended container isolation boundary to access resources outside it.

---

## 3. Network Ports

### What is a network port?

A network port is a numbered communication endpoint used by network applications and services.

An IP address identifies a network destination, while a port identifies a particular service endpoint.

Port numbers range from 0 to 65535 for TCP and UDP.

### Common ports

| Port | Common service | Purpose |
|---|---|---|
| 22 | SSH | Secure remote access |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web communication |
| 443 | HTTPS | Encrypted web communication |
| 8080 | HTTP alternative | Web applications and development servers |

These are common conventions, not guarantees of which service is running.

### Docker port mapping

Example:

```bash
docker run -d -p 8080:80 nginx
```

Command breakdown:

- `docker run`: Creates and starts a container.
- `-d`: Runs the container in the background.
- `-p`: Publishes a container port.
- `8080:80`: Maps host port 8080 to container port 80.
- `nginx`: The image being used.

A browser can then access the web server through:

```text
http://localhost:8080
```

### Security relevance

An unnecessarily exposed port can increase a system's **attack surface**.

Attack surface refers to the possible entry points an attacker might attempt to exploit.

Security professionals use tools such as Nmap to identify accessible ports and investigate the services running on them.

---

## 4. Cloud Computing

### What is cloud computing?

Cloud computing provides on-demand access to shared computing resources over a network.

Instead of purchasing and maintaining all physical infrastructure, organizations can obtain resources from providers such as Microsoft Azure, Amazon Web Services (AWS), and Google Cloud.

These resources can include:

- Virtual machines
- Storage
- Databases
- Networking
- Applications
- Security services

### Five essential characteristics of cloud computing

According to NIST:

**1. On-demand self-service**

Customers can provision computing resources when needed without direct human interaction with the provider.

**2. Broad network access**

Cloud services are accessible over networks using standard mechanisms.

**3. Resource pooling**

Providers use shared infrastructure to serve multiple customers while logically separating their resources.

**4. Rapid elasticity**

Resources can scale up or down quickly based on demand.

**5. Measured service**

Resource consumption can be monitored, measured, and reported.

### Advantages

- Reduced upfront hardware investment
- Faster deployment
- Flexible scaling
- Geographic availability
- Access to managed services
- Usage-based pricing options

### Disadvantages

- Ongoing costs can become expensive
- Dependence on internet connectivity
- Provider outages
- Vendor lock-in
- Security misconfigurations
- Less direct control over physical infrastructure

**Important:** Cloud computing does not eliminate hardware. The physical infrastructure is operated by the cloud provider.

---

## 5. Cloud Service Models

### IaaS — Infrastructure as a Service

The provider supplies computing infrastructure such as virtual machines, networking, and storage.

The customer typically manages the operating system, applications, and data.

Example: Azure Virtual Machines.

### PaaS — Platform as a Service

The provider manages more of the underlying infrastructure and application platform.

Developers focus primarily on deploying applications and managing their code and data.

Example: Azure App Service.

### SaaS — Software as a Service

The provider delivers a complete application that customers access over a network.

Example: Microsoft 365.

---

## 6. Shared Responsibility Model

Cloud security responsibilities are divided between the cloud provider and the customer.

### Cloud provider responsibilities

Depending on the service model, the provider commonly handles:

- Physical data centre security
- Physical server maintenance
- Underlying infrastructure
- Certain platform security controls

### Customer responsibilities

Depending on the service model, customers may be responsible for:

- User accounts and permissions
- Identity and Access Management (IAM)
- Data protection
- Application security
- Secure configurations
- Monitoring and access policies

### Practical scenario

A company hosts a database in Microsoft Azure.

An employee accidentally configures the database to allow unauthorized public access.

**Who is responsible?**

The company is generally responsible for correcting the access configuration because it controls those permissions.

The cloud provider securing the physical servers does not automatically prevent every customer misconfiguration.

**Security lesson:** Cloud security is a shared responsibility, not something completely handled by the provider.

---

## 7. My Understanding and Reflection

Today I learned how virtualization, containers, network ports, and cloud computing relate to modern IT infrastructure.

I understood that:

- Hypervisors allow virtual machines to operate on physical hardware.
- Containers are lightweight application environments that share the host kernel.
- Container images are templates used to create containers.
- Network ports identify communication endpoints for services.
- Cloud computing provides computing resources on demand.
- Cloud infrastructure can scale based on organizational needs.
- Cloud computing is not necessarily cheaper in every situation.
- Customers remain responsible for important security configurations.

### Knowledge assessment

I compared on-premises infrastructure with cloud computing and correctly identified:

- Reduced hardware maintenance
- Faster deployment
- Scalability
- Global accessibility
- Resource sharing
- Usage-based costs
- On-demand self-service

I also correctly identified the customer as the responsible party in a cloud database access misconfiguration scenario.

---

## 8. Topics to Review

- Differences between Type 1 and Type 2 hypervisors
- Container images versus running containers
- TCP and UDP ports
- Docker networking and port mapping
- IaaS, PaaS, and SaaS
- Cloud deployment models: public, private, and hybrid
- Shared Responsibility Model
- Identity and Access Management (IAM)

---

## 9. Next Learning Objectives

### Cybersecurity

Continue TryHackMe and begin connecting infrastructure concepts to practical security tasks.

Potential next topics:

- Linux fundamentals
- Networking fundamentals
- Cloud security basics
- Service enumeration
- Access control and IAM

