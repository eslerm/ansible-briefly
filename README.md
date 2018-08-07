# ansible-briefly

ansible-briefly is a rudimentary demonstration of an Ansible playbook and role.

It is important to inspect all the files in this repo and read their comments to understand how they fit together.

[slides](https://eslerm.github.io/ansible-briefly/)

## Key concepts

### Inventory

The `inventory` file contains groups of hosts and group variables. To use this playbook add your servers information to the inventory.

Authentication information can be set in the inventory or set when running `ansible-playbook`.

### Playbook

The file `briefly.yml` is an Ansible playbook.

The playbook can be ran with the inventory file by:
```
ansible-playbook -i inventory briefly.yml
```

Inspect `briefly.yml` to see how variabls and roles are set.


### Role

The `roles/` directory contains roles that the playbook can use. ansible-briefly uses a single role named `demo`.

Default role varialbes are set in `defaults/main.yml`. 

When the role is initiated the task `tasks/main.yml` runs. In this case  `main.yml` starts other tasks depending on the `editor` variable.

## Common `ansible-playbook` Parameters

### Variables

Variables set in the command line superceed all other variables.

This command will set the `editor` variable to `emacs` regardless of variables in the playbook or role:
```
ansible-playbook -i inventory --extra-vars="editor=emacs" briefly.yml
```

`ansible_ssh_user`, `ansible_ssh_private_key_file` and `ansible_ssh_pass` are variables which may be useful for server authentication. These variables can also be set in the `inventory` file.

### Privilege-escelatation password

A password is likely required to use sudo or other software-escalation software. `ansible-playbook` has a parameter to ask for this password:
```
ansible-playbook -i inventory --ask-become-pass briefly.yml
```

### Tags

When tags are set only tasks with the specified tags will run.

Example of using a tag:
```
ansible-playbook -i inventory -t vim briefly.yml
```

Note that the `message` task did not execute with the above command.
