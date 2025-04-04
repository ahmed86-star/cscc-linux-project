

# 🚀  Linux+ Project: Secure WordPress on AWS
 - Linux Administration**  
*Tiered AWS deployment with MariaDB backend and security validation*

[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?logo=amazon-aws&logoColor=white)](https://aws.amazon.com)
[![WordPress](https://img.shields.io/badge/WordPress-%2321759B.svg?logo=wordpress&logoColor=white)](https://wordpress.org)
[![MariaDB](https://img.shields.io/badge/MariaDB-003545?logo=mariadb&logoColor=white)](https://mariadb.org)

## 📋 Table of Contents
- [Architecture](#-architecture-overview)
- [Setup Guide](#-aws-setup-guide)
- [Security](#-security-configuration)
- [Validation](#-network-validation)
- [Deliverables](#-project-deliverables)

## 📊 Architecture Overview
```mermaid
graph TD
    A[🌐 Internet] -->|Ports 80/443| B[🖥️ Web Tier<br><sub>t3a.nano • Amazon Linux 2023</sub>]
    B -->|3306 → CSCI2790WebSG| C[🗃️ DB Tier<br><sub>t3a.nano • MariaDB 10.5</sub>]
    D[🔍 Validation Host] -.->|Blocked| C
    classDef web fill:#e1f5fe,stroke:#039be5
    classDef db fill:#e8f5e9,stroke:#43a047
    class B web; class C db
```
### week 1 ###

## 🛠️ AWS Setup Guide



 ### Security Groups ###
![all 3 security groups](https://github.com/user-attachments/assets/cdf88a07-4f14-438a-97a7-0c4bcaacacc7)

###  Web Server ###
![webhost](https://github.com/user-attachments/assets/4b832bfe-d6d3-4bd7-a068-b6c299387d7f)


```bash
# Web Server (CSCI2790WebSG)
- SSH (22): 0.0.0.0/0
- HTTP (80): 0.0.0.0/0
- HTTPS (443): 0.0.0.0/0
```
### Database ###

![DB host](https://github.com/user-attachments/assets/767a2083-70e8-4e0f-9416-8a13865a3535)

```
# Database (CSCI2790DBSG)
- SSH (22): 0.0.0.0/0
- MySQL (3306): CSCI2790WebSG
```
### Instance Deployment ##
![INSTANCES](https://github.com/user-attachments/assets/d008fe40-2485-4b74-847f-b51ccc90e28c)



### 2. Instance Deployment
```bash
# Web Server
AMI: Amazon Linux 2023
Type: t3a.nano
SG: CSCI2790WebSG

# Database Server
AMI: Amazon Linux 2023 
Type: t3a.nano
SG: CSCI2790DBSG
```

## 🔐 Security Configuration
```bash
# MariaDB Secure Installation
$ sudo mysql_secure_installation

# WordPress DB Setup
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'web-server-ip' IDENTIFIED BY 'StrongPass123!';
GRANT ALL ON wordpress.* TO 'wpuser'@'web-server-ip';
```

## 🔍 Network Validation
```bash
# From Validation Host (should fail)
$ telnet db-server-ip 3306
Connection timed out

# From Web Server (should succeed)
$ mysql -h db-server-ip -u wpuser -p
MariaDB [(none)]> STATUS
```











































































































































## 📚 Project Deliverables
| Component          | Details                                  |
|--------------------|------------------------------------------|
| Research Paper     | 10+ sources, tech comparisons           |
| Presentation       | Slides + live demo                       |
| AWS Configuration  | Functional 2-tier setup                 |
| Security Report    | Validation host results                 |

## 🚀 Quick Start
1. Clone repo:
   ```bash
   git clone https://github.com/yourusername/cscc-linux-project.git
   ```
2. Follow [Setup Guide](#-aws-setup-guide)
3. Verify with [Validation Tests](#-network-validation)



