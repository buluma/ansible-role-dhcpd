# Ansible role [dhcpd](https://galaxy.ansible.com/ui/standalone/roles/buluma/dhcpd/documentation)

Install and configure dhcpd on your system.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-dhcpd/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-dhcpd/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/dhcpd)](https://galaxy.ansible.com/ui/standalone/roles/buluma/dhcpd/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-dhcpd/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    dhcpd_subnets:
      - network: "{{ ansible_default_ipv4.network }}"
        netmask: "255.255.255.0"

  roles:
    - role: buluma.dhcpd
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-dhcpd/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: buluma.bootstrap
    - role: buluma.apt_autostart
    - role: buluma.core_dependencies
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-dhcpd/blob/master/defaults/main.yml):

```yaml
---
# defaults file for dhcpd

# Configuration settings for the daemon.
dhcpd_ipv4_interface: "{{ ansible_default_ipv4.interface | default('eth0') }}"

# Setting applicable for the global scope.
dhcpd_default_lease_time: 600
dhcpd_max_lease_time: 7200
dhcpd_subnet_mask: "255.255.255.0"
dhcpd_broadcast_address: "10.0.2.255"
dhcpd_routers: "10.0.2.254"
dhcpd_domain_name_servers:
  - "192.168.1.1"
  - "192.168.1.2"
dhcpd_domain_search: example.com

# The image to serve for PXE booting.
dhcpd_filename: "pxelinux.0"
# Where the image can be downloaded from.
dhcpd_next_server: "10.0.2.254"

# DHCP works with subnets, a list containing properties per subnet.
dhcpd_subnets:
  - network: "10.0.2.0"
    netmask: "255.255.255.0"
    range_start: "10.0.2.200"
    range_end: "10.0.2.210"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-dhcpd/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.apt_autostart](https://galaxy.ansible.com/buluma/apt_autostart)|[![Ansible Molecule](https://github.com/buluma/ansible-role-apt_autostart/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-apt_autostart/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-apt_autostart.svg)](https://github.com/shadowwalker/ansible-role-apt_autostart)|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Ansible Molecule](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-core_dependencies.svg)](https://github.com/shadowwalker/ansible-role-core_dependencies)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-dhcpd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Alpine](https://hub.docker.com/repository/docker/buluma/alpine/general)|all|
|[Amazon](https://hub.docker.com/repository/docker/buluma/amazonlinux/general)|Candidate|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|8|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-dhcpd/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-dhcpd/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-dhcpd/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)


Template inspired by [Robert de Bock](https://github.com/robertdebock)
