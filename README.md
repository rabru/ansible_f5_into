# Introduction, how to configure F5 over Ansible

This repository is built to be used in the [F5 Sandbox environment.](https://clouddocs.f5.com/training/automation-sandbox/) Please deploy the environment and login as student at the Ansible host, to clone this repository:

```
git clone https://github.com/rabru/ansible_f5AT.git
```

The inventory is already preconfigured here:

```
cat ~/networking-workshop/lab_inventory/hosts
```

You can validate it with:

```
ansible-inventory --list
```

To deploy a playbook, run the following command line:

```
ansible-playbook <playbook filename> -e target=f5 -e state=present
```

To remove the deployment you need to change the state to absent:

```
ansible-playbook <playbook filename> -e target=f5 -e state=absent
```

Since the AS3 deployments are deployed in seperate partitions, it is necessary to remove all Application, befor you can start the next one. This is, because we have only one external IP address, which can be configured only in one partition.

