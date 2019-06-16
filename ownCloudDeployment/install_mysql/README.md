install_mysql
=========

Ansible Role to install MySQL in a EC2 Instance

Requirements
------------

Pre-installed Python2 inside the EC2 Instance

Example Playbook
----------------

```yaml
  hosts: private_instance
  vars:
    ansible_python_interpreter: /usr/bin/python
  roles:
    - install_mysql
```

License
-------

BSD

Author Information
------------------

Danie Britto
