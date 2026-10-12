# Cybersecurity Learning Journal — Day 1: Ubuntu Home Lab & HTTP Fundamentals

**Date:** October 11, 2026  
**Focus:** Virtualization, Linux, VPN connectivity, networking, HTTP/HTTPS, and troubleshooting  
**Platform:** Ubuntu, VirtualBox, TryHackMe

## 1. Today's objectives

- Set up a personal cybersecurity lab using Ubuntu.
- Connect the virtual machine to TryHackMe using OpenVPN.
- Access and investigate a TryHackMe target.
- Understand basic HTTP communication and status codes.
- Develop a more systematic troubleshooting process.

## 2. Home lab setup

### Virtualization

Installed Oracle VirtualBox to run Ubuntu as a virtual machine (VM) inside a Windows computer.

**Terminology:**
- **Host OS:** The operating system running on the physical computer (Windows).
- **Guest OS:** The operating system running inside the virtual machine (Ubuntu).
- **Virtualization:** Technology that allows virtual computers to run on physical hardware.
- **VM:** A software-based computer with virtual CPU, RAM, storage, and network devices.

### Problems encountered

The Ubuntu VM experienced startup and display problems.

Troubleshooting included:
- Increasing video memory from 16 MB to 128 MB.
- Using the VMSVGA graphics controller.
- Disabling 3D acceleration.
- Investigating startup and installation delays.

**Lesson:** A virtual machine depends on correctly configured virtual hardware. When troubleshooting, change one setting at a time and observe the result.

## 3. Connecting Ubuntu to TryHackMe

Installed OpenVPN and downloaded a personal TryHackMe VPN configuration file.

Commands studied:

```bash
sudo apt update
sudo apt install openvpn -y
cd ~/Downloads
ls
sudo openvpn --config ./YOUR_CONFIG.ovpn
ip addr show tun0
```

**Terminology:**
- **VPN:** Virtual Private Network; establishes an encrypted network connection.
- **OpenVPN:** Software implementing a VPN connection.
- **`.ovpn`:** Configuration file containing settings for an OpenVPN connection.
- **`tun0`:** A virtual network interface commonly created by a VPN tunnel.
- **IP address:** A network address used to identify and communicate with devices.

**Result:** Established a VPN interface and successfully communicated with a TryHackMe target.

**Security note:** Never publish personal VPN configuration files or credentials on GitHub.

## 4. Network reconnaissance

Used Nmap to investigate a TryHackMe target.

```bash
nmap -sV TARGET_IP
nmap -sV -p 8080 TARGET_IP
```

**Terminology:**
- **Reconnaissance:** Gathering information about a system or network.
- **Enumeration:** Discovering specific information about services, resources, or configurations.
- **Port:** A numbered endpoint associated with a network service.
- **Service detection:** Identifying software or protocols running on open ports.

**Lesson:** An IP address identifies a network destination, while a port identifies a particular communication endpoint.

Only scan systems explicitly authorized for testing.

## 5. HTTP and HTTPS

### HTTP — Hypertext Transfer Protocol

Used for communication between web clients and servers.

- Common default port: 80
- Does not provide encryption by itself
- Supports methods such as GET and POST

### HTTPS — Hypertext Transfer Protocol Secure

HTTP protected using TLS encryption.

- Common default port: 443
- Encrypts HTTP communication
- Provides integrity protection and server authentication

**Important:** Ports 80 and 443 are defaults. Web servers can use other ports, including 8080.

### Commands investigated

```bash
curl http://TARGET_IP
curl -v http://TARGET_IP:8080
```

`curl` is a command-line tool for transferring data using protocols such as HTTP.

The `-v` option displays verbose connection and protocol information.

## 6. HTTP status codes

| Status | Meaning |
|---|---|
| 200 | OK — request succeeded |
| 301 | Moved Permanently |
| 304 | Not Modified |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 500 | Internal Server Error |

### HTTP 304 and caching

A browser cache stores previously downloaded resources so they can be reused.

When the browser asks whether a cached resource has changed, the server may respond with `304 Not Modified`.

Disabling the HTTP cache in Firefox Developer Tools can force fresh resource requests, often producing a `200 OK` response.

**Lesson:** HTTP 304 is not necessarily an error. It is part of normal web caching behavior.

## 7. Troubleshooting lessons

Problems investigated:
- Ubuntu VM startup issues.
- Linux command syntax and capitalization.
- Incorrect HTTP/HTTPS protocol selection.
- Using the wrong network port.
- Distinguishing TryHackMe's browser-based lab from a VPN-accessible target.
- Interpreting HTTP 405 and 304 responses.

### Troubleshooting framework

1. **Observe:** Record the exact error or behavior.
2. **Hypothesize:** Identify a possible explanation.
3. **Test:** Run one targeted experiment.
4. **Analyze:** Compare the result with the hypothesis.
5. **Conclude:** Document what the evidence supports.

Avoid changing multiple settings without understanding which change affected the outcome.

## 8. What I learned

- A virtual machine can function as a cybersecurity workstation.
- OpenVPN connects my lab to a remote network; it does not install target machines locally.
- HTTP and HTTPS are different protocols with different security properties.
- A reachable host does not necessarily provide a website on every port.
- HTTP status codes provide information about server behavior.
- Browser caching can change which HTTP responses appear during testing.
- Effective troubleshooting requires reasoning, not just copying commands.

## 9. Topics to review

- Linux terminal navigation and command syntax.
- IP addresses, ports, and protocols.
- DNS and hostname resolution.
- HTTP request and response headers.
- HTTP methods: GET, POST, PUT, DELETE.
- Nmap scan interpretation.

## 10. Next session

**Goal:** Complete Client-Server Basics and investigate HTTP requests independently.

Practice:
- Use Firefox Developer Tools to inspect network requests.
- Identify request methods, status codes, and headers.
- Compare browser requests with `curl`.
- Document observations, hypotheses, and conclusions.

**Reflection:** Today included substantial setup and troubleshooting. The next session should prioritize understanding the tools and concepts rather than repeatedly changing the lab configuration.