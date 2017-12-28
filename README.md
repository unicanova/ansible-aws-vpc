ansible-aws-vpc
=========

Simple Ansible role for management AWS VPC.
This role create:
 - AWS VPC
 - Subnets in region availability zones
 - IGW
 - Simple security group. Open tcp port 80, 443, 22 for world and all traffic for VPC cidkblock.

Requirements
------------

```sh
Ansible >= 2.4.0.0
boto
boto3
botocore
json
```


Role Variables
--------------
In vars/main.yml

```sh
Example vars

vpc:
  #Name of VPC 
  aws_vpc_name: "example-vpc"
  #AWS region for example
  aws_vpc_region: "eu-central-1"
  #AWS availability zones in region for example
  aws_vpc_az_a: "eu-central-1a"
  aws_vpc_az_b: "eu-central-1b"
  aws_vpc_az_c: "eu-central-1c"
  #AWS VPC cidr block for example
  aws_vpc_cidrblock: "10.0.0.0/16"
  #AWS VPC subnets in availability zone from vpc cidr block
  aws_vpc_subnet_az_a: "10.0.0.0/24"
  aws_vpc_subnet_az_b: "10.0.1.0/24"
  aws_vpc_subnet_az_c: "10.0.2.0/24"
```

Example Playbook
----------------

Export enviroment variables with AWS credentials:
```sh
export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
```

Create dir when you clone ansible role from github:
```sh
mkdir -p example/Roles
cd example
```

Clone role repository from github and configure ansible:
```sh
cd Roles
git clone https://github.com/unicanova/ansible-aws-vpc
cd ..
```

Edit ansible.cfg
```sh
[defaults]
hostfile = ./hosts.cfg
remote_user = root
host_key_checking = False
timeout = 5
pipelining = True
roles_path = Roles
```

Edit site.yaml
```sh
- hosts: 127.0.0.1
  connection: local
  roles:
   - { role: ansible-aws-vpc, tags: 'test' }
```

Run anisble:
```sh
ansible-playbook site.yaml -t test
```

License
-------

MIT

Author Information
------------------
Author: Sergey Ovsienko 

Email: so@unicanova.com

Company: UnicaNova 

Website: https://unicanova.com/
