Net-Add-Users
=============

Use Ansible core network modules to add users to a network device. 

Install:

```
ansible-galaxy -s https://galaxy-qa.ansible.com install ansible-testing.net-add-users
```

Requirements
------------

Requires the following components:

- Ansible 2.0 
- [privateip/ansible-modules/core working branch](https://github.com/privateip/ansible-modules-core/tree/working)
- net_config.py action plugin (not available publicly)


Role Variables
--------------

netuser_use_ssl:

> For non-SSH connections specifies whether or not to use SSL. Defaults to False.

netuser_username: 

> Account being created. 

netuser_password:

> Password for the account being created.

netuser_transport:

> Supported connection transports: cli, nxapi

netuser_delegate_to:

> Name of a host to delegate to. See [Ansible Delegation](http://docs.ansible.com/ansible/playbooks_delegation.html#delegation).   

netuser_users:

> List of users to be created. Each item will be an object with attributes: username, password, roles. The roles attribute is a list of role names.


Example Playbook
----------------

```
- name: Create users
  hosts: all
  connection: local
  vars:
      net_users:
          - { username: user,
              roles: ["network-operator", "network-admin"],
              password: <password>
            }
  roles:
      - { role: role-net-add-user,
          netuser_username: "{{ admin_username }}",
          netuser_password: "{{ admin_password }}",
          netuser_tranport: cli,
          netuser_delegate_to: "{{ delegate_to_host }}"
        }
```

License
-------

MIT

Author Information
------------------

Chris Houseknecht @chouseknecht

[RedHat | Ansible](http://www.ansible.com)
