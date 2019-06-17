# Creating a file share & sync solution using ownCloud and AWS

## What is ownCloud?

ownCloud is a suite of client–server software for creating and using file hosting services. ownCloud functionally has similarities to the widely used Dropbox. The primary functional difference between ownCloud and Dropbox is that ownCloud does not offer data centre capacity to host stored files

## Architecture

![alt Architecture Diagram](https://raw.githubusercontent.com/dannybritto96/Ansible-Playbooks/master/ownCloudDeployment/arch.jpeg)

## Role Descriptions

### Role 1: create-instances

- Creates a new key pair and saves it in a PEM file locally with it’s permission level set to 0400.
- Creates a VPC with CIDR 10.0.0.0/16
- Creates an Internet Gateway
- Creates a subnet with CIDR 10.0.2.0/24 (Public Subnet)
- Creates a subnet with CIDR 10.0.1.0/24 (Private Subnet)
- Creates an Elastic IP (for NAT gateway)
- Creates a NAT gateway which is then associated to the public subnet
- Edits the default route table to setup a route to 0.0.0.0/0 from NAT and associates the default route table to the private subnet.
- Creates a route table and adds route from 0.0.0.0/0 to Internet Gateway and this route table is associated to the public subnet.
- Creates a security group (for webserver) which allows port 22 and 80 to be accessible from anywhere in the internet.
- Creates another security group (for mysql server) which allows port 22 and 3306 connections only from the public subnet CIDR.
- Creating two instances, only in private subnet and public subnet.
- Private subnet is bootstrapped with a script to setup Python2 on the instance.
- Both the instances are added to different host groups.

### Role 2: install_mysql
(uses SSH tunneling via webserver)
- Updated apt cache
- Installs MySQL-Python module which is used by Ansible to run mysql_user and mysql_db modules.
- Uses mysql_user and mysql_db to configure MySQL for usage.
- Creates owncloud DB user and granting him to access only from the webserver instance.
- Edits the MySQL configuration to allow it to be accessible outside of localhost.
- Modifies firewall and IP tables to allow traffic.

### Role 3: install-owncloud

- Updates apt cache
- Installs Apache2 and PHP 7.1
- Adds owncloud repositories to sources.list
- Adds GPG keys from owncloud repos.
- Updated apt cache
- Installs owncloud and other related PHP modules.
- Changes DocumentRoot in Apache2 config file.
- Updates firewall
- Restarts Apache2
- Copies key file into the home directory.
