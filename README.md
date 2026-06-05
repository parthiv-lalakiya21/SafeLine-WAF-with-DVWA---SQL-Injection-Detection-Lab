# SafeLine WAF with DVWA - SQL Injection Detection Lab

## Project Overview

This project demonstrates how a Web Application Firewall (WAF) can protect a vulnerable web application from common web attacks such as SQL Injection.

A vulnerable application (DVWA) was deployed using Docker on Ubuntu Linux, and SafeLine WAF was configured as a Reverse Proxy to inspect, detect, and block malicious requests.

## Objectives

- Deploy DVWA using Docker
- Install and configure SafeLine WAF
- Configure Reverse Proxy protection
- Perform SQL Injection attacks
- Detect and block attacks using WAF
- Analyze attack logs and security events
- Implement HTTP Flood / Rate Limiting protection

---

## Lab Architecture

```text
User Browser
      │
      ▼
SafeLine WAF (Reverse Proxy)
      │
      ▼
DVWA (Docker Container)
```

---

## Technologies Used

- Ubuntu 22.04 LTS
- Docker
- DVWA (Damn Vulnerable Web Application)
- SafeLine WAF
- VirtualBox
- SQL Injection
- Reverse Proxy
- Web Security

---

## Installation

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/safeline-dvwa-lab.git
cd safeline-dvwa-lab
```

### 2. Deploy DVWA

Create `docker-compose.yml`

```yaml
version: '3'

services:
  dvwa:
    image: vulnerables/web-dvwa
    ports:
      - "8080:80"
    restart: always
```

Run:

```bash
docker-compose up -d
```

Verify:

```bash
docker ps
```

---

### 3. Install SafeLine WAF

Install SafeLine WAF using the official installer.

```bash
sudo bash -c "$(curl -fsSLk https://waf.chaitin.com/release/latest/setup.sh)"
```

Access Dashboard:

```text
https://localhost:9443
```

---

### 4. Configure Reverse Proxy

Application Settings:

| Field | Value |
|---------|---------|
| Domain | localhost |
| Listening Port | 80 |
| Upstream | http://127.0.0.1:8080 |
| Mode | Reverse Proxy |

---

## SQL Injection Testing

Navigate to:

```text
DVWA → SQL Injection
```

Payload Used:

```sql
1' OR '1'='1
```

Expected Result:

- SafeLine detects attack
- Request blocked
- Attack log generated

---

## Attack Detection

SafeLine successfully detected:

- SQL Injection
- Malicious URL patterns
- Suspicious request payloads

Example Log:

```text
Action: Blocked
Attack Type: SQL Injection
IP Address: 127.0.0.1
```

---

## HTTP Flood Protection

Configured rate-limiting policies to mitigate excessive requests.

Example test:

```bash
for i in {1..300}; do curl http://localhost; done
```

---

## Screenshots

### DVWA Application

Add screenshot here:

```text
screenshots/dvwa-home.png
```

### SafeLine Dashboard

Add screenshot here:

```text
screenshots/safeline-dashboard.png
```

### SQL Injection Detection

Add screenshot here:

```text
screenshots/sql-injection-blocked.png
```

### Attack Logs

Add screenshot here:

```text
screenshots/attack-logs.png
```

---

## Skills Gained

- Linux Administration
- Docker Containerization
- Web Application Security
- SQL Injection Testing
- WAF Deployment
- Reverse Proxy Configuration
- HTTP Flood Protection
- Security Monitoring
- Log Analysis

---

## Project Outcome

Successfully implemented SafeLine WAF to protect a Docker-hosted DVWA application. The WAF detected and blocked SQL Injection attacks, monitored malicious traffic, and generated detailed security logs for analysis.

---

## Author

**Parthiv Lalakiya**

Cybersecurity Enthusiast | SOC Analyst Aspirant

LinkedIn: Add Your LinkedIn Profile

GitHub: Add Your GitHub Profile
