# Ansible Cross-OS Automation Project

A practical Ansible automation project for managing Linux systems across **Ubuntu, Amazon Linux, and Red Hat** from a centralized Ansible control node.

The project demonstrates how automation can be organized around operating-system groups while using SSH-based remote management.

## 🎯 Project Goal

The goal is to automate configuration across different Linux distributions without manually repeating administration tasks on every server.

```text
                    Ansible Control Node
                           │
                    ┌──────▼──────┐
                    │    Ansible  │
                    │  Playbooks  │
                    └──────┬──────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
          Ubuntu      Amazon Linux      Red Hat
```

## 🖥️ Inventory Structure

The inventory organizes systems into operating-system groups:

```ini
[control]
control-node-ubuntu

[ubuntu_workers]
worker-ubuntu

[redhat]
worker-redhat

[amazon]
worker-amazon

[workers:children]
ubuntu_workers
redhat
amazon
```

This makes it possible to target:

* All workers
* Ubuntu workers
* Amazon Linux
* Red Hat
* Control node

## 📁 Repository Structure

```text
Ansible_Cross_OS_Automation_Project/
├── playbooks/
├── hosts.ini
└── README.md
```

## 🧰 Technology Stack

| Area          | Technology   |
| ------------- | ------------ |
| Automation    | Ansible      |
| Control Node  | Ubuntu       |
| Target OS     | Ubuntu       |
| Target OS     | Amazon Linux |
| Target OS     | Red Hat      |
| Remote Access | SSH          |
| Inventory     | INI          |
| Configuration | YAML         |
| Environment   | AWS EC2      |

## 🔐 Test Connectivity

Before running automation:

```bash
ansible all -i hosts.ini -m ping
```

A successful response confirms that Ansible can connect to the managed hosts.

## ▶️ Run Playbooks

Run against all workers:

```bash
ansible-playbook \
  -i hosts.ini \
  playbooks/<playbook>.yml
```

Ubuntu only:

```bash
ansible-playbook \
  -i hosts.ini \
  playbooks/<playbook>.yml \
  --limit ubuntu_workers
```

Amazon Linux:

```bash
ansible-playbook \
  -i hosts.ini \
  playbooks/<playbook>.yml \
  --limit amazon
```

Red Hat:

```bash
ansible-playbook \
  -i hosts.ini \
  playbooks/<playbook>.yml \
  --limit redhat
```

## 🔍 Useful Commands

```bash
ansible all -i hosts.ini -m ping
```

```bash
ansible-inventory -i hosts.ini --graph
```

```bash
ansible workers -i hosts.ini -m command -a "uname -a"
```

```bash
ansible workers -i hosts.ini -m setup
```

Run with verbose output:

```bash
ansible-playbook \
  -i hosts.ini \
  playbooks/<playbook>.yml \
  -v
```

## 🧠 Cross-OS Automation

Different Linux distributions can have different:

* Package managers
* Service names
* File locations
* Default configurations

Ansible can handle these differences through:

* Inventory groups
* Facts
* Variables
* Conditional tasks
* Tags
* OS-specific tasks

Example:

```yaml
when: ansible_os_family == "Debian"
```

or:

```yaml
when: ansible_os_family == "RedHat"
```

## 🧪 Troubleshooting

```text
Check inventory
      ↓
Test SSH
      ↓
Run ansible ping
      ↓
Check facts
      ↓
Check permissions
      ↓
Run playbook with -v
      ↓
Verify configuration
```

## 📌 Skills Demonstrated

* Ansible
* Inventory management
* SSH automation
* Linux administration
* Cross-OS automation
* YAML
* Ansible facts
* Conditional execution
* Playbook troubleshooting
* AWS EC2 management

## 🔗 Terraform + Ansible

The project also demonstrates an important DevOps workflow:

```text
Terraform
   ↓
Provision AWS Infrastructure
   ↓
EC2 Instances
   ↓
Ansible
   ↓
Configure Servers
```

Terraform handles **infrastructure provisioning**, while Ansible handles **server configuration**.

## 👨‍💻 Author

**Sanket Shinde**

GitHub: https://github.com/Sanket4404
