title: Creating Graphs
author:
  name: Mark Esler
  twitter: markesler
  url: https://eslerm.github.io
output: index.html
#style: style.css
#layout: layout.mustache
theme: sjaakvandenberg/cleaver-dark

--

# Ansible
## Briefly Stated

--

### What is Ansible

Ansible is a tool for automating system adminsitration tasks.

It can deploy new servers and manage existing servers. *e.g.*:
- Install Galaxy with a PostgreSQL database and NGINX web server to a fresh operating system.
- Backup production server, upgrade server files, upgrade database, test, and bring back online.

--

### YAML Example

Install vim with [Ansible's yum module](https://docs.ansible.com/ansible/latest/modules/yum_module.html)

```
# yum module example

- name: "Install vim"
  hosts: vim-host
  yum:
    name: vim
    state: latest
  when: editor != "emacs"
  become: yes
```

--

### Demo of YAML Example

```
ansible-playbook -i inventory demo.yml
```

--

### Common Anisble Organization

Ansible is often organized into **inventories**, **roles**, and **playbooks**.
- **Inventories** define groups of servers and group specific variables.

- **Roles** are a collection of tasks, templates, and variables used to perform a certain job.
  - Roles are meant to be reusbale for many applications.
  - *e.g.* install and configure PostgreSQL

--

### Common Anisble Organization **cont.**

- **Playbooks** define a specific application of roles for groups of hosts.
  - Playbook variables override role variables which can change which tasks of the role execute.
  - *e.g.* two playbooks which use a Galaxy role, but one deploys a web server and the other deploys a job handler server.

--

### Reasons to use Ansible

- Automation.
- Administration becomes programmatic.
  - Management becomes reproducible.
  - Removes most human error.
  - Code is easy to share and audit.
- Only requires SSH and Python on remote machine.

--

### More info

Anisble has [great documentation](#).

[An example playbook and role](#) are shared with this slideshow.

The [Galaxy Project](#) has built roles for Galaxy.

--

### Inventory example

Contents of `inventory`:

```
[vim-hosts]
1.2.3.4

[vim-hosts:vars]
ansible_ssh_private_key_file=/path/to/my/private.key
```

--

### Role example

Below is the file list of the `demo` role:
```
###
```

--

### Playbook example:

Contents of `demo.yml`
```
###
```

Run this playbook with:
```
ansible-playbook -i inventory demo.yml
```

An alternative playbook (`demo-alt.yml`) installs `emacs` instead of `vim`.
