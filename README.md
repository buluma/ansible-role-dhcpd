# [Ansible role dhcpd](#ansible-role-dhcpd)

Install and configure dhcpd on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-dhcpd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-dhcpd/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-dhcpd/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-dhcpd)|[![downloads](https://img.shields.io/ansible/role/d/buluma/dhcpd)](https://galaxy.ansible.com/buluma/dhcpd)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-dhcpd/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

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
  gather_facts: false
  become: true

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

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.apt_autostart](https://galaxy.ansible.com/buluma/apt_autostart)|[![Build Status GitHub](https://github.com/buluma/ansible-role-apt_autostart/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-apt_autostart/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-apt_autostart/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-apt_autostart)|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-dhcpd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Alpine](https://hub.docker.com/r/buluma/alpine)|all|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-dhcpd/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-dhcpd/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

