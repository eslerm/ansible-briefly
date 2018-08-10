# Briefly Anisble

Briefly Ansible was written so that people learning Ansible have a working demonstration that they can play and experiment with. Please read [Ansible's Documentaion](https://docs.ansible.com/) if you intend to use Ansible meaningfully.

A high level overview of Ansible is provided in these [slides](https://eslerm.github.io/briefly-ansible/).

## Key concepts

### Inventory

The `inventory` file contains groups of hosts and group variables. To use this playbook add your servers information to the inventory.

Authentication information can be set in the inventory or set when running `ansible-playbook`.

See Ansible's User Guide [Working with Inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html).

### Playbook

The file `briefly.yml` is an Ansible playbook.

The playbook can be run with the inventory file:
```
ansible-playbook -i inventory briefly.yml
```

Run the above command a second time and look for differences in the standard output.

See Ansible's User Guide [Intro to Playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html) for more.

### Role

The `roles/` directory contains roles which the playbook can use. Briefly Ansible uses a single role named `demo`.

`demo`'s defaults are are set in `roles/demo/defaults/main.yml`. 

When the role is initiated the task `roles/demo/tasks/main.yml` runs. In this case `main.yml` prints a debug message and then starts other tasks depending on the `editor` variable.

See Ansible's User Guide [Roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html) for more.

## `ansible-playbook` 

Below are a few useful `ansible-playbook` parameters. Read Ansible's [ansible-playbook](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html) documentation for more.

### `--extra-vars`

Variables set in the command line supersedes all other variables.

This command will set the `editor` variable to `gvim` regardless of what `editor` is set to in the playbook or role:
```
ansible-playbook -i inventory --extra-vars="editor=gvim" briefly.yml
```

### `--ask-become-pass`

Set this if privilege-escelation software, like `sudo`, requires a password:
```
ansible-playbook -i inventory --ask-become-pass briefly.yml
```

### `--tags` or `-t`

When tags are set only tasks with the specified tags will run.


In this example only tasks tagged as `vim` will run. The `Debug message` task has no tags and will not run:
```
ansible-playbook -i inventory -t vim briefly.yml
```

In this example, only `gvim` tagged tasks will start. The single task with the `gvim` tag will be skipped since, it fails the condtion that variable `editor` must be set to `gvim`.
```
ansible-playbook -i inventory -t gvim --extra-vars="editor=emacs" briefly.yml
```
