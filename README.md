Role: cns.ec2
========

This role initializes ec2 instances and assigns tags to instances.

Requirements
------------

Nothing, it runs out of the box.

Role Variables
--------------

In the current version, you can specify the following variables:

| Name               | Default |                                                        |
|--------------------|---------|--------------------------------------------------------|
| site_prefix        |   ---   | Prefix to use for AWS object naming.                   |
| keypair            |   ---   | AWS registered SSH keypair to install on EC2 instance  |
| region             |   ---   | Region in which the resource exists.                   |
| zone               |   ---   | Availability zone in which the resource exists.        |
| name               |   ---   | Name of EC2 instance.                                  |
| owner              |   ---   | EC2 instance owner for billing.                        |
| instance           |   ---   | Object containing instance details (see example).      |

Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by Sam Morrison [@samcns](https://www.twitter.com/samcns)

Examples
--------

```yaml
---
- name: cns.ec2 role test
  hosts: all
  roles:
    - cns.ec2
```

```yaml
---
# Dict containing instance configuration details
instance_web:
  ec2:
    # New EC2 instance role (web, app, git, etc.)
    role: web
    # Environment: dev, test, stage, or prod
    mode: dev
    # Prefix override 
    prefix: "{{ site_prefix }}"
    # Name of EC2 instance
    name: "{{ prefix }}-{{ role }}-{{ mode }}"
    # Keypair override
    keypair: "{{ keypair }}"
    # Region override 
    region: "{{ region }}"
    # Owner override 
    owner: "{{ owner }}"
    # Base AMI image for EC2 instance
    ami_image: ami-9c621234
    # EC2 Instance type
    instance_type: t1.micro
    # Assign a public IP address
    assign_public_ip: yes
    # Total number of instances for this type
    count: 1
```
