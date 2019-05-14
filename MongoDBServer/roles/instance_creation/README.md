EC2 Instance Creation
=========

Create an EC2 instance, VPC, Subnet, Internet Gateway and a Route Table.

Requirements
------------

boto

Role Variables
--------------

| variable | Description |
| --- | --- |
| region | Region in which the resources must be created |
| group_name | Name of security group |
| rules | Rules for the security group |
| instance_type | Instance type. Ex. t2.micro |
| image | AMI ID |
| keypair | Name of keypair to be created |
| count | Number of VMs to be spun off |
| instance_tags | Tags for the instance |

Example Playbook
----------------

```yaml
  - name: Provision an EC2 Instance
    hosts: localhost
    gather_facts: False
    tags: Provisioning

    roles:
      - instance_creation
```

License
-------

BSD

Author Information
------------------

Danie Britto
