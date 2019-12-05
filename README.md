mysql
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-mysql"> <img src="https://travis-ci.org/robertdebock/ansible-role-mysql.svg?branch=master" alt="Build status"/></a> <img src="https://img.shields.io/ansible/role/d/22971"/> <img src="https://img.shields.io/ansible/quality/22971"/>

Install and configure mysql on your system.

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.mysql
      mysql_databases:
        - name: my_db
          encoding: utf8
          collation: utf8_bin
      mysql_users:
        - name: my_user
          password: my_pass
          priv: "my_db.*:ALL"
```

The machine you are running this on, may need to be prepared, I use this playbook to ensure everything is in place to let the role work.
```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
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

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/mysql.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tag|allow_failures|
|---------|---|--------------|
|amazonlinux|latest|no|
|debian|unstable|yes|
|debian|latest|no|
|centos|7|no|
|centos|latest|no|
|fedora|latest|no|
|fedora|rawhide|yes|
|opensuse|latest|no|
|ubuntu|latest|no|

This role has been tested on these Ansible versions:

- ansible>=2.8, <2.9
- ansible>=2.9
- git+https://github.com/ansible/ansible.git@devel

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | The PyMySQL (Python 2.7 and Python 3.X) or MySQL-python (Python 2.X) module is required. |
| amazonlinux:1 | /etc/init.d/mysqld: line 16: /etc/sysconfig/network: No such file or directory |


Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-mysql) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-mysql/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

Modules
-------

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

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
