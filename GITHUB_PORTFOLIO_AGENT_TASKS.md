# GitHub Portfolio Improvement Tasks

This file is a practical task list for an automation agent or for manual cleanup. The goal is to make the GitHub profile look like a real junior Linux / network / infrastructure engineer portfolio, not like a random collection of lab files.

Owner: Rajabali Rahimov  
GitHub: https://github.com/RM7hsh

---

## Global rules

1. Do not remove working code.
2. Do not commit passwords, private keys, real IP addresses, tokens or personal infrastructure data.
3. Replace secrets with examples and document them as variables.
4. Prefer clear documentation over flashy text.
5. Keep README files honest: lab, test, competition, or production-like must be clearly separated.
6. Every public repository must answer three questions quickly:
   - What problem does this solve?
   - What technologies are used?
   - How can someone run or inspect it?

---

## Repository standard

Every public repo should contain:

```text
README.md
.gitignore
LICENSE
CHANGELOG.md
SECURITY.md
docs/
  screenshots/
  architecture.md
examples/
```

Optional, when useful:

```text
docs/diagrams/
Makefile
requirements.yml
.env.example
inventory.example.ini
inventory.example.yml
```

---

## Standard README structure

Use this structure for all infrastructure repositories:

```md
# Project Name

Short one-paragraph description.

## What this project does

- Feature 1
- Feature 2
- Feature 3

## Architecture

Explain nodes, services, ports, networks and data flow.

## Technology stack

- Linux / OS
- Ansible / Terraform / Docker / etc.
- Monitoring / database / network tools

## Repository structure

Explain important folders and files.

## Quick start

Commands required for a lab run.

## Verification

Commands or screenshots proving the result.

## Security notes

Explain secret handling and lab-only assumptions.

## Roadmap

What should be improved next.
```

---

## Profile repository: RM7hsh/RM7hsh

### Tasks

- Keep `README.md` as the main profile page.
- Add badges only if they do not make the profile look childish.
- Add links to the four strongest repositories:
  - ansible-monitoring-automation
  - redos-itplanet-ansible-lab
  - terraform-ansible-docker-lab
  - linux-server-baseline-check
- Add a short Russian version if needed: `README.ru.md`.
- Add screenshots only if they are clean and do not expose secrets.

---

## Repo: ansible-monitoring-automation

### Goal

Make this the strongest public repository. It should show that Rajabali can automate monitoring infrastructure with Ansible.

### Tasks

1. Rename the title in README from test-style wording to professional wording.
2. Keep the warning that it is not production-ready, but move it into `Security notes`.
3. Add `inventory.example.ini` and `inventory_dynamic.example.ini`.
4. Ensure all real credentials are removed from repo history if any existed.
5. Add `.gitignore` rules:

```gitignore
*.retry
.automation_last_inputs.env
ssh_keys/
*.pem
*.key
*.pub
inventory_dynamic.ini
.env
.vault_pass
```

6. Add `SECURITY.md` explaining:
   - do not store passwords in inventory;
   - use Ansible Vault;
   - rotate keys if they were committed;
   - avoid exposing Prometheus/Grafana without auth/TLS.
7. Add `docs/architecture.md` with this topology:

```text
Ansible control node
  -> Prometheus server :9090
  -> Grafana server :3000
  -> Linux targets :9100 node_exporter
  -> Windows targets :9182 windows_exporter
```

8. Add screenshots:
   - Grafana datasource
   - Linux dashboard
   - Windows dashboard
   - successful Ansible run

9. Add roadmap:
   - Ansible Vault
   - TLS for Grafana/Prometheus
   - CI linting
   - Molecule tests
   - role split into reusable roles

---

## Repo: redos-itplanet-ansible-lab

### Goal

Present this as a competition-style RED OS infrastructure automation project.

### Tasks

1. Fix local absolute paths in README, for example `/Users/rm7/...` must become relative links.
2. Add `docs/architecture.md` with server/client/services overview.
3. Add `docs/competition-context.md` explaining that this is a lab/competition solution, not a production deployment.
4. Add `.env.example` or `group_vars/example.yml` for variables.
5. Move sensitive variable names into examples only.
6. Add `SECURITY.md` with notes about passwords, SSH hardening and firewall rules.
7. Add screenshots or sanitized terminal outputs for:
   - Samba domain users
   - DHCP lease
   - Nextcloud page
   - Squid auth/blocking check
   - firewalld zones
8. Add a short English summary at the top, but keep detailed Russian documentation.

---

## Repo: terraform-ansible-docker-lab

### Goal

Show a clean DevOps/infrastructure lab: Terraform creates VMs, Ansible configures them, Docker runs applications.

### Tasks

1. Add `docs/architecture.md` with this flow:

```text
Terraform -> Proxmox VMs -> generated inventory -> Ansible -> Docker hosts -> Registry -> Runtime app
```

2. Add `terraform/` examples if this repo currently contains only Ansible side.
3. Add `inventory.example.ini` instead of relying only on local symlink paths.
4. Add `Makefile` with commands:

```makefile
ping:
	ansible docker_hosts -m ping

docker:
	ansible-playbook playbooks/docker-site.yml

registry:
	ansible-playbook playbooks/registry-site.yml

app:
	ansible-playbook playbooks/runtime-app-site.yml
```

5. Add `SECURITY.md` explaining that the HTTP Docker Registry is lab-only and production should use TLS/auth.
6. Add screenshots or outputs:
   - `terraform apply` summary
   - `ansible docker_hosts -m ping`
   - registry catalog
   - app page from runtime host
7. Add CI later for YAML linting and shellcheck.

---

## Repo: linux-server-baseline-check

### Goal

Make this a small but clean beginner-friendly Bash project.

### Tasks

1. Keep README simple and professional.
2. Add `shellcheck` compatibility.
3. Add `--json` output mode.
4. Add `--interface eth0` option.
5. Add disk warning threshold option, for example `--disk-warn 80`.
6. Add tests with simple mocked command outputs if possible.
7. Add example output to `docs/examples.md`.

---

## GitHub profile settings to change manually

These settings cannot be changed reliably through file edits and should be done in GitHub UI.

### Pin repositories in this order

1. `ansible-monitoring-automation`
2. `redos-itplanet-ansible-lab`
3. `terraform-ansible-docker-lab`
4. `linux-server-baseline-check`

### Add topics

#### ansible-monitoring-automation

`ansible`, `prometheus`, `grafana`, `monitoring`, `node-exporter`, `windows-exporter`, `linux`, `automation`, `devops`

#### redos-itplanet-ansible-lab

`ansible`, `redos`, `samba-ad`, `linux`, `nextcloud`, `squid`, `iredmail`, `firewalld`, `competition`

#### terraform-ansible-docker-lab

`terraform`, `ansible`, `docker`, `proxmox`, `docker-registry`, `devops`, `infrastructure-as-code`

#### linux-server-baseline-check

`bash`, `linux`, `server`, `health-check`, `qemu-guest-agent`, `systemd`

---

## Final quality checklist

A repository is portfolio-ready when:

- README explains the goal in the first 5 lines.
- There is no real password or private key.
- Quick start commands are copy-pasteable.
- Screenshots or terminal outputs prove that it works.
- Architecture is understandable without reading all code.
- Lab-only limitations are clearly stated.
- The project name looks professional.
