# Ansible Cheatsheet

> Ansible automates configuration management, application deployment, and orchestration over SSH or other transports.

## Table of Contents
- [Ad-Hoc Commands](#ad-hoc-commands)
- [Inventory](#inventory)
- [Playbooks](#playbooks)
- [Modules](#modules)
- [Roles](#roles)
- [Vault](#vault)
- [Galaxy](#galaxy)
- [Facts](#facts)
- [Variables & Tags](#variables--tags)
- [Debugging](#debugging)

## Ad-Hoc Commands

| Command | Description |
| --- | --- |
| `ansible all -i inventory.ini -m ping` | Test connectivity to every host in an inventory. |
| `ansible all -i inventory.ini -a "uptime"` | Run an uptime command on every host. |
| `ansible web -i inventory.ini -b -m apt -a "name=nginx state=present update_cache=yes"` | Install Nginx on hosts in the web group with privilege escalation. |
| `ansible db -i inventory.ini -m service -a "name=postgresql state=restarted"` | Restart PostgreSQL on hosts in the db group. |
| `ansible all -i inventory.ini -m command -a "hostnamectl"` | Run a command without invoking a shell. |
| `ansible all -i inventory.ini -m shell -a "df -h | tail -n +2"` | Run a shell command when shell features are required. |
| `ansible all -i inventory.ini -m setup` | Gather facts from every managed host. |
| `ansible all -i inventory.ini --limit web01 -m ping` | Restrict an ad-hoc command to a single host. |
| `ansible all -i inventory.ini --check -m file -a "path=/tmp/example state=touch"` | Preview module changes in check mode when supported. |
| `ansible all -i inventory.ini --ask-become-pass -b -m ping` | Prompt for the privilege-escalation password before running. |

## Inventory

| Command | Description |
| --- | --- |
| `ansible-inventory -i inventory.ini --list` | Display the parsed inventory as JSON. |
| `ansible-inventory -i inventory.ini --list --yaml` | Display the parsed inventory as YAML. |
| `ansible-inventory -i inventory.ini --graph` | Render the inventory group hierarchy as a graph. |
| `ansible-inventory -i inventory.ini --graph web` | Render the hierarchy rooted at the web group. |
| `ansible-inventory -i inventory.ini --host web01` | Show inventory variables resolved for one host. |
| `ansible -i inventory.ini all --list-hosts` | List hosts selected by an Ansible pattern. |

## Playbooks

| Command | Description |
| --- | --- |
| `ansible-playbook -i inventory.ini site.yml` | Run a playbook against the specified inventory. |
| `ansible-playbook -i inventory.ini site.yml --syntax-check` | Check playbook syntax without executing tasks. |
| `ansible-playbook -i inventory.ini site.yml --check` | Simulate supported changes without applying them. |
| `ansible-playbook -i inventory.ini site.yml --check --diff` | Show file diffs for supported changes in check mode. |
| `ansible-playbook -i inventory.ini site.yml --limit web` | Run the playbook only against hosts in the web group. |
| `ansible-playbook -i inventory.ini site.yml --tags deploy` | Run only tasks tagged deploy. |
| `ansible-playbook -i inventory.ini site.yml --skip-tags slow` | Skip tasks tagged slow. |
| `ansible-playbook -i inventory.ini site.yml --start-at-task="Configure Nginx"` | Start execution at a named task. |
| `ansible-playbook -i inventory.ini site.yml --step` | Prompt before each task is executed. |
| `ansible-playbook -i inventory.ini site.yml --list-tasks` | List tasks selected for each play without running them. |
| `ansible-playbook -i inventory.ini site.yml --list-tags` | List tags defined in the playbook. |
| `ansible-playbook -i inventory.ini site.yml --flush-cache` | Clear cached facts for targeted hosts before execution. |

## Modules

| Command | Description |
| --- | --- |
| `ansible web -i inventory.ini -b -m copy -a "src=./index.html dest=/var/www/html/index.html"` | Copy a local file to web hosts. |
| `ansible web -i inventory.ini -b -m template -a "src=nginx.conf.j2 dest=/etc/nginx/nginx.conf"` | Render and deploy a Jinja2 template. |
| `ansible all -i inventory.ini -b -m file -a "path=/opt/app state=directory mode=0755"` | Create a directory with the requested permissions. |
| `ansible all -i inventory.ini -b -m user -a "name=deploy groups=www-data append=yes"` | Create or update a deployment user. |
| `ansible web -i inventory.ini -b -m get_url -a "url=https://example.com/app.tar.gz dest=/tmp/app.tar.gz"` | Download a file to managed hosts. |
| `ansible all -i inventory.ini -b -m package -a "name=curl state=present"` | Install a package through the platform package manager. |
| `ansible web -i inventory.ini -b -m uri -a "url=http://localhost/ status_code=200"` | Make an HTTP request and assert an expected response code. |
| `ansible all -i inventory.ini -m debug -a "msg='reachable'"` | Print a diagnostic message for selected hosts. |

## Roles

| Command | Description |
| --- | --- |
| `ansible-galaxy role init roles/webserver` | Create a standard role directory structure. |
| `ansible-galaxy role list` | List installed Galaxy roles. |
| `ansible-galaxy role install geerlingguy.nginx` | Install a role from Ansible Galaxy. |
| `ansible-galaxy role remove geerlingguy.nginx` | Remove an installed Galaxy role. |

## Vault

| Command | Description |
| --- | --- |
| `ansible-vault create group_vars/all/vault.yml` | Create a new encrypted vault file in an editor. |
| `ansible-vault edit group_vars/all/vault.yml` | Edit an encrypted vault file. |
| `ansible-vault view group_vars/all/vault.yml` | Decrypt and display a vault file without editing it. |
| `ansible-vault encrypt group_vars/all/secrets.yml` | Encrypt an existing plaintext file. |
| `ansible-vault decrypt group_vars/all/secrets.yml` | Decrypt a vault file in place. |
| `ansible-vault rekey group_vars/all/vault.yml` | Change the password used to encrypt a vault file. |
| `ansible-vault encrypt_string --name db_password 'secret-value'` | Encrypt one variable value for embedding in YAML. |
| `ansible-vault create --vault-id dev@prompt group_vars/all/dev-vault.yml` | Create a vault using a named vault identity. |
| `ansible-playbook -i inventory.ini site.yml --ask-vault-pass` | Prompt for the vault password when running a playbook. |
| `ansible-playbook -i inventory.ini site.yml --vault-password-file .vault_pass` | Read the vault password from a local file. |

## Galaxy

| Command | Description |
| --- | --- |
| `ansible-galaxy collection init my_namespace.my_collection` | Create a new collection skeleton. |
| `ansible-galaxy collection build` | Build a collection artifact from galaxy.yml. |
| `ansible-galaxy collection install community.general` | Install a collection from Ansible Galaxy. |
| `ansible-galaxy collection install -r requirements.yml` | Install collections declared in a requirements file. |
| `ansible-galaxy collection install ./my_namespace-my_collection-1.0.0.tar.gz` | Install a collection from a local artifact. |
| `ansible-galaxy collection list` | List installed collections. |
| `ansible-galaxy role install -r requirements.yml` | Install roles declared in a requirements file. |
| `ansible-galaxy role search nginx` | Search Ansible Galaxy roles by keyword. |

## Facts

| Command | Description |
| --- | --- |
| `ansible all -i inventory.ini -m setup` | Gather the complete fact set from selected hosts. |
| `ansible all -i inventory.ini -m setup -a "filter=ansible_distribution*"` | Gather only facts matching a filter. |
| `ansible all -i inventory.ini -m setup -a "gather_subset=!all,min"` | Gather a minimal fact subset for faster runs. |
| `ansible-inventory -i inventory.ini --host web01 --yaml` | Inspect host variables resolved from inventory sources. |

## Variables & Tags

| Command | Description |
| --- | --- |
| `ansible-playbook -i inventory.ini site.yml -e "environment=staging"` | Set an extra variable with high precedence. |
| `ansible-playbook -i inventory.ini site.yml -e @vars/staging.yml` | Load extra variables from a YAML or JSON file. |
| `ansible-playbook -i inventory.ini site.yml --tags "deploy,config"` | Run tasks matching either listed tag. |
| `ansible-playbook -i inventory.ini site.yml --tags all` | Run all tagged and untagged tasks selected by the play. |
| `ansible-playbook -i inventory.ini site.yml --skip-tags "never"` | Skip tasks marked with the never tag. |
| `ansible-playbook -i inventory.ini site.yml --list-tags` | Review available tags before selecting a run. |

## Debugging

| Command | Description |
| --- | --- |
| `ansible-playbook -i inventory.ini site.yml -v` | Run a playbook with verbose output. |
| `ansible-playbook -i inventory.ini site.yml -vvv` | Run a playbook with connection and task debugging detail. |
| `ansible-playbook -i inventory.ini site.yml -vvvv` | Include maximum connection debugging output. |
| `ansible-config dump --only-changed` | Show Ansible configuration values changed from defaults. |
| `ansible-doc ping` | Display documentation for the ping module. |
| `ansible-doc -s ansible.builtin.copy` | Show a short parameter synopsis for the copy module. |
