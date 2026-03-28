# Ansible Infrastructure Automation

A collection of production-ready Ansible playbooks and roles for automated infrastructure configuration, environment setup, and application deployment across Linux hosts. Covers idempotent configuration management patterns used in enterprise DevOps workflows — from base server hardening to Kubernetes node provisioning.

## Repo Structure

```
ansible-automation/
├── roles/
│   ├── common/         # Base server setup, hardening, sysctl
│   ├── docker/         # Docker CE installation and configuration
│   ├── kubernetes/     # kubeadm, kubelet, kubectl installation
│   └── monitoring/     # Node exporter, CloudWatch agent
├── playbooks/
│   ├── provision-servers.yml       # Full server provisioning
│   ├── install-docker.yml          # Docker-only setup
│   ├── setup-kubernetes-nodes.yml  # K8s node prep
│   └── deploy-monitoring.yml       # Monitoring agent setup
├── inventory/
│   ├── hosts.yml                   # Static inventory
│   ├── group_vars/                 # Variables per group
│   └── host_vars/                  # Variables per host
└── scripts/
    └── run-playbook.sh             # Wrapper with vault support
```

## Key Features

- **Idempotent** — safe to run multiple times with no unintended changes
- **Role-based** — reusable, composable roles across any playbook
- **Environment-aware** — separate var files per environment (dev/staging/prod)
- **Dynamic AWS inventory** — auto-discovers EC2 instances by tag
- **Vault-ready** — sensitive variables encrypted with Ansible Vault
- **CI/CD integrated** — triggered post Terraform provisioning

## Usage

```bash
# Full server provisioning
ansible-playbook -i inventory/hosts.yml playbooks/provision-servers.yml

# Target a specific environment
ansible-playbook -i inventory/hosts.yml playbooks/provision-servers.yml \
  --limit dev_servers

# Run with vault for encrypted secrets
ansible-playbook -i inventory/hosts.yml playbooks/provision-servers.yml \
  --ask-vault-pass

# Dry run (check mode)
ansible-playbook -i inventory/hosts.yml playbooks/provision-servers.yml \
  --check --diff
```

## Roles Overview

| Role | What It Does |
|---|---|
| `common` | Updates packages, sets timezone, configures sysctl, disables swap, creates users |
| `docker` | Installs Docker CE, configures daemon, manages service |
| `kubernetes` | Installs kubeadm/kubelet/kubectl, configures cgroup driver |
| `monitoring` | Deploys node exporter and CloudWatch agent |

## Author

**Djamal Tighilt Ferhat** — DevOps & Cloud Engineer
[github.com/dtighiltferhat](https://github.com/dtighiltferhat)
