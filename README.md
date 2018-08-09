# Briefly Anisble

Briefly Ansible was written to aid learning the fundamentals of Ansible through a desriptive and rudimentary demonstation of Ansible. Please read [Ansible's Documentaion](https://docs.ansible.com/) if you intend to use Ansible meaningfully.

All files of Briefly Ansible should to be read so, that the reader can interpret how they fit together.

A high level overview of Ansible is provided in these [slides](https://eslerm.github.io/briefly-ansible/).

## Key concepts

### Inventory

The `inventory` file contains groups of hosts and group variables. To use this playbook add your servers information to the inventory.

Authentication information can be set in the inventory or set when running `ansible-playbook`.

See Ansible's User Guide to [Working with Inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html).

### Playbook

The file `briefly.yml` is an Ansible playbook.

The playbook can be run with the inventory file with:
```
ansible-playbook -i inventory briefly.yml
```

Run the above command a second time and look for differences in the standard output.

See Ansible's User Guide to [Intro to Playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html) for more.

### Role

The `roles/` directory contains roles which the playbook can use. Briefly Ansible uses a single role named `demo`.

`demo`'s defaults are are set in `roles/demo/defaults/main.yml`. 

When the role is initiated the task `roles/demo/tasks/main.yml` runs. In this case `main.yml` prints a debug message and then starts other tasks depending on the `editor` variable.

See Ansible's User Guide to [Roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html) for more.

## `ansible-playbook` 

See Ansible's [ansible-playbook](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html) dcoumentation for more.

### `--extra-vars`

Variables set in the command line supersedes all other variables.

This command will set the `editor` variable to `gvim` regardless of variables in the playbook or role:
```
ansible-playbook -i inventory --extra-vars="editor=gvim" briefly.yml
```

### `--ask-become-pass`

Set this if privilege-escelation software, like `sudo`, requires a password:
```
ansible-playbook -i inventory --ask-become-pass briefly.yml
```

### `--tags` or `-t`

When tags are set only tasks with the specified tags will run:
```
ansible-playbook -i inventory -t vim briefly.yml
```

Note that the `Debug message` task does not execute when tags are used.

In this example, only `gvim` tagged tasks will be initiated, but will be skipped since, the `editor` variable is not set to `gvim`:
```
ansible-playbook -i inventory -t gvim --extra-vars="editor=emacs" briefly.yml
```

## Essential Reading

[Ansible's User Guide](https://docs.ansible.com/ansible/latest/user_guide/index.html).
