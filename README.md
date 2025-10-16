# Ansible Tutorial
Ansible tutorial playbook repository

## Basics
- Create an inventory file and input the IPV4 address or the hostname of the machines to be controlled.
- Make sure that these machines are accessible via SSH Keys.

## Basic commands
``` bash
ansible all --key-file <ssh_private_key_file_location> -i <inventory_file> -m <module>
```

``` bash
ansible all --key-file <ssh_private_key_file_location> -i <inventory_file> -m <module> -a <attribute>
ansible all --key-file <ssh_private_key_file_location> -i <inventory_file> -m <module> -a "<attribute1> <attribute2>"
```

## Config file
- A config file can be created to give the starter parameters by naming it `ansible.cfg`.
- There are many locations to create this file.
- Check the [documentation](https://docs.ansible.com/ansible/latest/reference_appendices/config.html) for further configuration settings
- A basic config file might include:
```
[defaults]
inventory=<inventory_file>
private_key_file=<ssh_private_key_file_location>
remote_user=<remote user to be used to execute ansible commands>
```

- Since the config file mentions two of the parameters written in the command, the command can be simplified.
``` bash
ansible all --key-file -m <module> -a <attribute>
ansible all --key-file -m <module> -a "<attribute1> <attribute2>"
```

## sudo Commands
- To use modules that require super user privilages, the `--become --ask-become-pass`
``` bash
ansible all -m dnf -a "name=* state=latest" --become --ask-become-pass
```

- This will update all the systems in the inventory file and use sudo for it.

## Playbook commands
- Create a yml playbook with the correct syntax specified in the documentation.
- Run the following command the execute the playbook:
``` bash
ansible-playbook <playbook_file.yml>
```
## Host variables
- One can also create variables specific to hosts by creating host variables.
- Create a directory called `host_vars`.
- Create YAML files in the names of hosts in the inventory. Eg: `192.168.1.50.yml`.
- Inside the file declare the variable and the value. Eg: `package: package_name`.
- Once declared, the variable can be called in the playbook and its value will change according to the host. Eg: `"{{package}}"`. Must be in double quotes `" "`.

