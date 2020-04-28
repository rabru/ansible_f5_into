# Introduction, how to configure F5 over Ansible

This repository is built to be used in the [F5 Sandbox environment.](https://clouddocs.f5.com/training/automation-sandbox/) Please deploy the environment and login as student at the Ansible host, to clone this repository:

```
git clone https://github.com/rabru/ansible_f5_intro.git
```

The inventory is already preconfigured here:

```
cat ~/networking-workshop/lab_inventory/hosts
```

You can validate it with:

```
ansible-inventory --list
```

## How to deploy playbooks
If you deploy a playbook regarding the device management of the BIG-IP, you can deploy it over the following command line: 

```
ansible-playbook <playbook filename> -e target=f5
```
If you would like to deploy elements related to an application deployment, you need to specify if you would like to create or remove the deployment. For this Ansible use the state variable.
To start a playbook to create an application deployment, run the following command line:

```
ansible-playbook <playbook filename> -e target=f5 -e state=present
```

To remove the deployment, you need to change the state to absent:

```
ansible-playbook <playbook filename> -e target=f5 -e state=absent
```

Since the AS3 deployments are deployed in separate partitions, it is necessary to remove all Application before you can start the next one. This is, because we have only one external IP address, which can be configured only in one partition.

## Install AS3 Extension

Before we can install the AS3 extension at the BIG-IP, we need to download the install package. You can find the extension [here](https://github.com/F5Networks/f5-appsvcs-extension/releases). 

Be aware, that the path will change over time:
```
cd files/

# Long Time Supported version:
wget https://github.com/F5Networks/f5-appsvcs-extension/releases/download/v3.13.2/f5-appsvcs-3.13.2-1.noarch.rpm

# Latest version:
wget https://github.com/F5Networks/f5-appsvcs-extension/releases/download/v3.19.0/f5-appsvcs-3.19.0-4.noarch.rpm
```

Please adapt the AS3Version variable at the AS3_install.yaml playbook.

Next you can install the package on the target BIG-IP:

```
ansible-playbook AS3_install.yaml -e target=f5
```

