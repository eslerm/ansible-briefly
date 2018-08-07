title: ansible-briefly slides
author:
  name: Mark Esler
  url: https://eslerm.github.io
output: index.html
theme: sjaakvandenberg/cleaver-dark

--

# ansible-briefly

<img src="https://raw.githubusercontent.com/eslerm/slides-ansible-briefly_stated/master/qr.gif" style="width: auto; position: absolute; bottom: 1em; right: 1em;"/>

--

### What is Ansible

Ansible is a tool for automating system adminsitration tasks.

It can be used to deploy new servers and manage existing servers. *e.g.*:
- Install Galaxy with a PostgreSQL database and NGINX web server to a fresh operating system.
- Backing up a production server, upgrade its software  & database, test, and relaunch.

--

### Ansible YAML Example
```yaml
# yum module example

- hosts: vim-host             # hostgroup to run playbook on
  vars:
    editor: vim               # custom variables
  tasks:
  - name: "Install vim"       # task description for standard output
    yum:                      # Ansible module
      name: vim                 # package to install
      state: latest             # use latest version
    when: editor == "vim"   # run when variable 'editor' is set to 'vim'
    become: yes               # run as a priviledge-escelated user
```

--

### Demo of Ansible YAML Example

```bash
ansible-playbook -i inventory vim.yml
```

--

### Common Anisble Organization

Ansible is often organized with **inventories**, **roles**, and **playbooks**.

- **Inventories** define groups of servers and group specific variables.

- **Roles** are a reusable collection of tasks, templates, and variables used to perform a certain job.

--

### Common Anisble Organization **cont.**

- **Playbooks** define a specific application of roles for a group of hosts.
  - Playbook variables override role variables which can change which tasks of the role execute.
  - *e.g.* two playbooks could use a Galaxy role, but one deploys a web server and the other deploys a job handler server.

--

### Reasons to use Ansible

- For server build automation.

- Administration becomes programmatic.
  - Build is reproducible.
  - Build process is readily shareable and auditiable.

- Only requires SSH and Python on remote machine.

--

### More info

Anisble has [great documentation](#).

[ansible-briefly](#) is a desriptively commened Ansible example/

The [Galaxy Project](#) has built roles for Galaxy.

--

### Inventory example

Contents of `inventory`:

```ini
[vim-hosts]
1.2.3.4

[vim-hosts:vars]
ansible_ssh_private_key_file=/path/to/my/private.key
```

--

### Role example

Below is the file list of the `demo` role:
```yaml
###
```

--

### Playbook example:

Contents of `demo.yml`
```yaml
###
```

```bash
ansible-playbook -i inventory demo.yml
```

An alternative playbook (`demo-alt.yml`) installs `emacs` instead of `vim`.
