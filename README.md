acl_manager
===========

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

* `block_ip` - This block/blacklist a source IP address from accessing a destination IP address.
* `unblock_ip` - This unblock/whitelist a Network address or Host address.
* `block_url` - This block/blacklist a URL feed/address from being accessed.
* `unblock_url` - This unblock/whitelist a URL feed/address, which in turn can be accessed without being blocked.

Example Playbook
----------------

* `Checkpoint block IP address`

```
- hosts: checkpoint
  connection: httpapi

  tasks: 
    - include_role:
        name: acl_manager
        tasks_from: block_ip
      vars:
        source_ip: 192.168.0.10
        destination_ip: 192.168.0.11
        ansible_network_os: checkpoint
```

* `Cisco FTD unblock Network address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: unblock_ip
      vars:
        unblock_network_type: network
        unblock_name: permit_network
        unblock_subtype: NETWORK
        unblock_value: 192.168.1.0/24
        ansible_network_os: cisco_ftd
```

* `Cisco FTD block Network address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: block_ip
      vars:
        block_network_type: network
        block_name: block_network
        block_subtype: NETWORK
        block_value: 192.168.2.0/24
        ansible_network_os: cisco_ftd
```

* `Cisco FTD unblock URL address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: unblock_url
      vars:
        unblock_url_type: url
        unblock_name: GoogleURL
        unblock_url_description: URL for Google
        unblock_url: www.google.com

        ansible_network_os: cisco_ftd
```

* `Cisco FTD block URL address`

```
- hosts: ftd
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: block_url
      vars:
        block_url_type: url
        block_name: Attacker_Url
        block_url_description: Detected Attacker URL
        block_url: www.attacker.com
        ansible_network_os: cisco_ftd
```

* `FortiOS block IP address`

```
- hosts: fortios
  connection: httpapi

  tasks:
    - include_role:
        name: acl_manager
        tasks_from: block_ip
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
