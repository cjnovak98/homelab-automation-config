# homelab-automation-config
This repo serves to be an example configuration of my homelab-automation collection.


# Ansible Configuration

## ansible.cfg
The Ansible configuration in this repo was generated using 

`ansible-config init --disabled > ansible.cfg`

This generates an ansible.cfg with all options filled out, and commented out.

The only things included is disabling host key checking and searching for an inventory file located in `inventory/inventory.ini`


# How to use this repo

This repo is a template config repo for executing against the [homelab-automation](https://github.com/cjnovak98/homelab-automation) Ansible collection (hosted only on Git)

## Introduction

Let's begin by familiarizing with the directory structure of this repo

```
.
├── collections  - Contains Ansible-galaxy requirements.yaml
├── inventory - Contains example inventory from my homelab
└── playbooks - Self explanatory. Contains various ansible playbooks.
    ├── auth_keys - Contains public keys to be installed every user
    └── group_vars/all - Used to configure Ansible vars
```

For someone who is not used to Ansible, I'll explain a few fundementals.

1. The ansible.cfg sets global configurations for Ansible. In the configuration I am using, `inventory/inventory.ini` contains an INI file formatted host inventory. There are 2 groups in this inventory called `workstations` and `hypervisors`. When executing Ansible, you need to define the target hosts. for instance, if I ran `ansible -m ping all` this would ping all of the hosts in the inventory. If I only wanted to check hypervisors I would run `ansible -m ping hypervisors`.
1. This repo makes use of a core Ansible feature called a "Collection" more info can be found at the [official documentation here](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_structure.html) The TL;DR is: An Ansible Collection is a logical structure for packaging up a collection of Ansible modules, variables or "scripts" for lack of better words. This can then be installed using the `ansible-galaxy` CLI, so it can be executed like a package.


The `cnovak.homelab_automation` collection contains many roles. For information on Ansible roles, [look here](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

Of those roles, here are their following functions

* `cnovak.homelab_automation.common` - This is a "common" role that is executed before any other role, no matter which role is executed. This includes things like setting up NFS mounts and ensuring a standard set of packages are installed no matter what the system.
* `cnovak.homelab_automation.configure_users` - The purpose of this role is to create or configure a standard set of user accounts, with trusted public keys for SSH access, and ensure user group access for any hypervisors in the environment. `wheel` and `libvirt` being key in my environment.
* `cnovak.homelab_automation.create_vm` - 
* `cnovak.homelab_automation.hypervisor_config` -
* `cnovak.homelab_automation.sushy` - 


## Instructions


