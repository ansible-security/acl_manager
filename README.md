acl_manager
===========

# This content is currently under development and should not be considered production ready

An [Ansible](https://ansible.com) role to manage access control lists for many firewall devices.

Current supported list of providers:
* checkpoint
* Cisco FTD
* FortiOS

Requirements
------------
Red Hat Enterprise Linux 7.x, or derived Linux distribution such as CentOS 7,
Scientific Linux 7, etc

Functions
---------

* `blacklist_ip` - This blacklist a source IP address from accessing a destination IP address.
* `whitelist_ip` - This whitelist a Network address or Host address.
* `blacklist_url` - This blacklist a URL feed/address from being accessed.
* `whitelist_url` - This whitelist a URL feed/address, which in turn can be accessed without being blocked.

Example Playbook
----------------

* `Checkpoint blacklist IP address`

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
        ansible_network_os: checkpoint
```

* `Cisco FTD whitelist Network address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: whitelist_ip
      vars:
        whitelist_network_type: network
        whitelist_name: permit_network
        whitelist_subtype: NETWORK
        whitelist_value: 192.168.1.0/24
        ansible_network_os: cisco_ftd
```

* `Cisco FTD blacklist Network address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: blacklist_ip
      vars:
        blacklist_network_type: network
        blacklist_name: block_network
        blacklist_subtype: NETWORK
        blacklist_value: 192.168.2.0/24
        ansible_network_os: cisco_ftd
```

* `Cisco FTD whitelist URL address`

```
- hosts: checkpoint
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: whitelist_url
      vars:
        whitelist_url_type: url
        whitelist_name: GoogleURL
        whitelist_url_description: URL for Google
        whitelist_url: www.google.com
        ansible_network_os: cisco_ftd
```

* `Cisco FTD blacklist URL address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: blacklist_url
      vars:
        blacklist_url_type: url
        blacklist_name: Attacker_Url
        blacklist_url_description: Detected Attacker URL
        blacklist_url: www.attacker.com
        ansible_network_os: cisco_ftd
```

* `FortiOS blacklist IP address`

```
- hosts: fortios
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: blacklist_ip
      vars:
        policy_id: 10
        policy_name: block_ip_test_example_policy
        source_interface: any
        destination_interface: any
        source_ip: ip_test_example
        destination_ip: all
        service: HTTP
        policy_schedule: always
        policy_logtraffic: all
        policy_logtraffic_start: disable
```


License
-------

GPLv3

Author Information
------------------

[Ansible Security Automation Team](https://github.com/ansible-security)
