# IBM MQ Active-Passive Automation using Ansible
## Overview

This repository provides **100% automated deployment and management of IBM MQ in an Active-Passive High Availability configuration using Ansible**.

The project follows Ansible best practices by implementing a **role-based architecture**, making it reusable, modular, maintainable, and idempotent. Every stage of the IBM MQ lifecycle—from storage preparation to installation, configuration, startup, shutdown, and removal—is fully automated.

The automation is designed for enterprise environments where consistency, repeatability, and minimal manual intervention are required.

---

# Features

- Fully automated IBM MQ installation
- Active-Passive HA deployment
- Modular role-based Ansible architecture
- Idempotent playbooks
- Reusable roles
- Centralized variable management
- Easy customization
- Automated prerequisite installation
- Automated storage creation and mounting
- Automated user and group creation
- MQ configuration automation
- Queue Manager creation
- Start and Stop automation
- MQ removal automation
- Production-ready project structure
- Minimal manual intervention

---

# Project Structure

```
.
├── inventories/
│   ├── production/
│   └── dev/
│
├── group_vars/
├── host_vars/
│
├── roles/
│   ├── create-storage/
│   ├── setupusers/
│   ├── prepare_install/
│   ├── installmq/
│   ├── configure/
│   ├── startmq/
│   ├── stopmq/
│   ├── deletemq/
│   └── ...
│
├── ibm-mq.yml
├── startmq.yml
├── stopmq.yml
├── deletemq.yml
└── README.md
```

---

# Architecture

```
                +----------------------+
                |    Inventory Hosts   |
                +----------+-----------+
                           |
                           |
                    ibm-mq.yml
                           |
      ------------------------------------------------
      |              |             |                 |
      |              |             |                 |
Create Storage   Setup Users   Install Prereqs   Install MQ
      |              |             |                 |
      -----------------------------------------------
                           |
                     Configure MQ
                           |
                   Create Queue Manager
                           |
                     Validate Installation
                           |
                    Ready for Production
```

---

# Playbooks

## 1. ibm-mq.yml

This is the primary deployment playbook.

It performs:

- Storage creation
- Filesystem preparation
- MQ user creation
- Prerequisite installation
- IBM MQ installation
- MQ configuration
- Queue Manager creation
- Final validation

Execute:

```bash
ansible-playbook -i inventories/production ibm-mq.yml
```

---

## 2. startmq.yml

Starts the IBM MQ services and Queue Managers.

```bash
ansible-playbook startmq.yml
```

---

## 3. stopmq.yml

Gracefully stops IBM MQ services.

```bash
ansible-playbook stopmq.yml
```

---

## 4. deletemq.yml

Completely removes IBM MQ installation.

This playbook performs:

- Queue Manager removal
- Service cleanup
- Package removal
- Files cleanup
- Storage cleanup (optional)

```bash
ansible-playbook deletemq.yml
```

---

# Roles

| Role | Description |
|------|-------------|
| create-storage | Creates disks, filesystems and mount points |
| setupusers | Creates MQ users and required groups |
| prepare_install | Installs operating system prerequisites |
| installmq | Installs IBM MQ packages |
| configure | Configures IBM MQ and Queue Managers |
| startmq | Starts MQ services |
| stopmq | Stops MQ services gracefully |
| deletemq | Removes MQ installation and cleanup |

---

# Industry Standard Practices Used

This project follows enterprise automation best practices.

## Modular Design

Each responsibility is isolated into its own Ansible Role.

Instead of one large playbook, every task has a dedicated role making maintenance significantly easier.

---

## Idempotent Automation

Playbooks can be executed multiple times safely.

Running the deployment again will only apply necessary changes.

---

## Separation of Responsibilities

Installation, configuration, storage, user creation, startup and removal are completely separated.

This improves readability and maintainability.

---

## Reusable Roles

Every role is independent and reusable across different environments.

For example:

- Install MQ only
- Configure existing installation
- Only start MQ
- Only stop MQ

without executing unnecessary tasks.

---

## Inventory-Based Deployments

Supports multiple environments such as:

- Development
- Testing
- UAT
- Production

using separate inventories.

---

## Centralized Configuration

Configuration values are managed through:

- group_vars
- host_vars
- variables

instead of hardcoding values.

---

## Easy Maintenance

Adding a new configuration requires changes only in the corresponding role instead of modifying the entire automation.

---

## Scalable Architecture

Additional roles can easily be added for:

- MQ Clustering
- SSL Configuration
- Monitoring
- Backup Automation
- Disaster Recovery
- Queue Creation
- Channel Configuration

without changing existing code.

---

# Prerequisites

- Ansible 2.12+
- Linux Servers
- IBM MQ Installation Packages
- SSH Connectivity
- Sudo Privileges
- Python installed on managed hosts

---

# Deployment Workflow

```
Create Storage
        │
        ▼
Create MQ User
        │
        ▼
Install Prerequisites
        │
        ▼
Install IBM MQ
        │
        ▼
Configure MQ
        │
        ▼
Create Queue Manager
        │
        ▼
Start MQ
        │
        ▼
Validate Installation
```

---

# Example Usage

Deploy IBM MQ

```bash
ansible-playbook ibm-mq.yml
```

Start MQ

```bash
ansible-playbook startmq.yml
```

Stop MQ

```bash
ansible-playbook stopmq.yml
```

Remove MQ

```bash
ansible-playbook deletemq.yml
```

---

# Advantages

- Enterprise ready
- Fully automated deployment
- High availability support
- Repeatable deployments
- Easy maintenance
- Modular architecture
- Reusable roles
- Production-ready structure
- Faster deployments
- Reduced human error
- Consistent server configuration

---

# Future Enhancements

Some possible enhancements include:

- IBM MQ Clustering
- TLS/SSL Automation
- Multi-instance Queue Managers
- Monitoring integration (Prometheus/Grafana)
- IBM MQ REST API configuration
- CI/CD pipeline integration (Jenkins/GitHub Actions)
- Molecule testing for Ansible roles
- Automated health checks
- Backup and restore automation

---

# Contributing

Contributions, suggestions, and improvements are welcome. Feel free to open an issue or submit a pull request.

---

# License

This project is released under the MIT License.

---

## Author

**Salah Abbasi**

Senior Platform Engineer | DevOps | Kubernetes | AWS | Ansible | IBM MQ

---

⭐ If you found this repository useful, consider giving it a **Star**.
