# [eclipse](#eclipse)

Install eclipse and plugins on your system.

|Travis|GitHub|GitLab|Quality|Downloads|Version|
|------|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-eclipse.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-eclipse)|[![github](https://github.com/robertdebock/ansible-role-eclipse/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-eclipse/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-eclipse/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-eclipse)|[![quality](https://img.shields.io/ansible/quality/45618)](https://galaxy.ansible.com/robertdebock/eclipse)|[![downloads](https://img.shields.io/ansible/role/d/45618)](https://galaxy.ansible.com/robertdebock/eclipse)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-eclipse.svg)](https://github.com/robertdebock/ansible-role-eclipse/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.eclipse
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.java
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for eclipse

# The release to install.
# See https://www.eclipse.org/downloads/packages/release
eclipse_release: 2019-12

# The release version to install, either: R, RC1, M3, M2 or M1.
eclipse_release_version: R

# The type of installation, either: jee, committers, cpp, dsl, java, javascript, jee, modeling, parallel, php, rcp, rust, scout or testing.
eclipse_release_type: java

eclipse_install_path: /tmp

eclipse_plugins:
  # This plugin causes an issue:
  # org.eclipse.m2e.logback.configuration:
  # The org.eclipse.m2e.logback.configuration bundle was activated before
  # the state location was initialized.  Will retry after the state location
  # is initialized.
  # - name: org.tigris.subversion.subclipse.feature.group
  #   repository: "http://subclipse.tigris.org/update_1.10.x"
  - name: org.sonatype.m2e.egit.feature.feature.group
    repository: "https://repo1.maven.org/maven2/.m2e/connectors/m2eclipse-egit/0.15.1/N/0.15.1.201806191431"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-eclipse/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |
| [robertdebock.java](https://galaxy.ansible.com/robertdebock/java) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-java.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-java) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-java/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-java/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/eclipse.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|amazon|Candidate|
|el|7, 8|
|debian|buster, bullseye|
|fedora|all|
|opensuse|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| alpine | [Errno 2] No such file or directory: 'eclipse' |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-eclipse) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-eclipse/issues)

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

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
