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

### Methods

How do we make our lab infrastructure easier to maintain?

Ho do we export our lab infrastructure to other labs?

--

### Ansible

Ansible is a tool for automating system adminsitration tasks.

--

### Ansible YAML Example
```
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

```
ansible-playbook -i inventory vim.yml
```

--

### Advantages of Ansible

- reproducible
- shareable
- auditable

--

### More info

Anisble has [great documentation](#).

[ansible-briefly](#) is a desriptively commened Ansible example/

The [Galaxy Project](#) has built roles for Galaxy.

