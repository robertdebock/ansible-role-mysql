mysql
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-mysql"><img src="https://travis-ci.org/robertdebock/ansible-role-mysql.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure mysql on your system.

<img src="https://img.shields.io/ansible/role/d/22971"/>
<img src="https://img.shields.io/ansible/quality/22971"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    mysql_databases:
      - name: my_db
        encoding: utf8
        collation: utf8_bin
    mysql_users:
      - name: my_user
        password: my_pass
        priv: "my_db.*:ALL"

  roles:
    - robertdebock.mysql
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - robertdebock.bootstrap
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for mysql

# The address mysql should bind to.
mysql_bind_address: 127.0.0.1

# This role can populate databases and users, see below.
# mysql_databases:
#   - name: firstdb
#   - name: seconddb
#
# mysql_users:
#   - name: firstuser
#     password: MyPaSsWoRd
#     priv: "firstdb.*:ALL"
#     host: some.host.name
#   - name: seconduser
#     password: MyPaSsWoRd2
#     priv: "seconddb.*:ALL"
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

This role uses the following modules:
```yaml
---
- command
- ini_file
- meta
- mysql_db
- mysql_user
- package
- service
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/mysql.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.7|ansible 2.8|ansible devel|
|------------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes*|
|alpine-latest|yes|yes|yes*|
|archlinux|yes|yes|yes*|
|centos-7|yes|yes|yes*|
|centos-latest|yes|yes|yes*|
|debian-stable|yes|yes|yes*|
|debian-unstable*|yes|yes|yes*|
|fedora-latest|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes*|
|opensuse-leap|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes*|
|ubuntu-rolling|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.




Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-mysql) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-mysql/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
