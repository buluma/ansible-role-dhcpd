# [dhcpd](#dhcpd)

Install and configure dhcpd on your system.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-dhcpd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-dhcpd/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-dhcpd/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-dhcpd)|[![quality](https://img.shields.io/ansible/quality/58372)](https://galaxy.ansible.com/buluma/dhcpd)|[![downloads](https://img.shields.io/ansible/role/d/58372)](https://galaxy.ansible.com/buluma/dhcpd)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-dhcpd.svg)](https://github.com/buluma/ansible-role-dhcpd/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
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

The machine needs to be prepared. In CI this is done using `molecule/default/prepare.yml`:
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


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
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

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-dhcpd/blob/main/requirements.txt).

## [Status of used roles](#status-of-requirements)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.apt_autostart](https://galaxy.ansible.com/buluma/apt_autostart)|[![Build Status GitHub](https://github.com/buluma/ansible-role-apt_autostart/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-apt_autostart/actions)|[![Build Status GitLab ](https://gitlab.com/buluma/ansible-role-apt_autostart/badges/main/pipeline.svg)](https://gitlab.com/buluma/ansible-role-apt_autostart)|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab ](https://gitlab.com/buluma/ansible-role-bootstrap/badges/main/pipeline.svg)](https://gitlab.com/buluma/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab ](https://gitlab.com/buluma/ansible-role-core_dependencies/badges/main/pipeline.svg)](https://gitlab.com/buluma/ansible-role-core_dependencies)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-dhcpd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|alpine|all|
|amazon|Candidate|
|el|8|
|debian|all|
|fedora|all|
|ubuntu|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some roles can't run on a specific distribution or version. Here are some exceptions.

| variation                 | reason                 |
|---------------------------|------------------------|
| Suse | Starting ISC DHCPv4 Server chown: invalid user: 'dhcpd:root
shadow
... |


If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-dhcpd/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-dhcpd/blob/master/CHANGELOG.md)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
