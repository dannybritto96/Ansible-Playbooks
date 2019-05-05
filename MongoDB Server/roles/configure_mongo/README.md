configure_mongo
=========

Installing MongoDB and setting it up for remote connection

Role Variables
--------------

| variable | Description |
| --- | --- |
| admin_username | Username of admin of DB Instance |
| admin_pwd | Admin Password |
| dbname | Name of collection to be created |
| username | User for the created collection |
| pwd | Password for user of the created collection |

Example Playbook
----------------

```yaml
    - name: Configure EC2
        hosts: all
        vars:
          ansible_ssh_private_key_file: "{{ playbook_dir }}/keypair.pem"
          ansible_ssh_user: ubuntu
          ansible_python_interpreter: /usr/bin/python3
        roles:
          -  configure_mongo
```
License
-------

BSD

Author Information
------------------

Danie Britto