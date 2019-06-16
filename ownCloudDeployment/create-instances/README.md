create-instances
=========

Create two EC2 Instances, one DB Server in Private Subnet and another Bastion Server / Jump Server which also acts as the Web Server.

Role Variables
--------------

| variable | Description |
| --- | --- |
| region | AWS Region |
| vpc_cidr | CIDR block of VPC |
| private_cidr | CIDR block of Private Subnet |
| public_cidr | CIDR block of Public Subnet |
| instance_type | AWS Instance Type |
| Image | AMI ID |
| private_sg | Private Security Group Name |
| Image | Public Security Group Name |


Example Playbook
----------------

```yaml
    - hosts: localhost
      roles:
         - create-instances
```
License
-------

BSD

Author Information
------------------

Danie Britto
