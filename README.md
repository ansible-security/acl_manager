acl_manager
===========

# This content is currently under development and should not be considered production ready

An [Ansible](https://ansible.com) role to manage access control lists for many firewall devices.

Current supported list of providers:
* checkpoint

Requirements
------------
Red Hat Enterprise Linux 7.x, or derived Linux distribution such as CentOS 7,
Scientific Linux 7, etc

Functions

* `blacklist_ip` - This blacklist a source IP  address from accessing a destination IP address

Example Playbook
----------------

```
- hosts: checkpoint
  connection: httpapi

  tasks: 
    - include_role:
        name: acl_manager
        tasks_from: blacklist_ip
      vars:
        source_ip: 192.168.0.10
        destination_ip: 192.168.0.11
        firewall_provider: checkpoint
```


License
-------

GPLv3

Author Information
------------------

[Ansible Security Automation Team](https://github.com/ansible-security)
