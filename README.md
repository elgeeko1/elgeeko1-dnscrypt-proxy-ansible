# Ansible role to deploy dockerized dnscrypt-proxy
Features:
- dnscrypt-proxy preconfigured for quad9
- runs in bridged network mode (as opposed to insecure host mode)
- (optional) ipv6 enabled using variable `dnscrypt_proxy_use_ipv6: true`

# Requirements
Provisioning host:
- ansible 2.9 or later

Host that will run dnscrypt-proxy:
- OS that can be provisioned by Ansible (this role is tested with Ubuntu 18.04)
- docker
 - An ansible role for installing docker is available from https://github.com/elgeeko1/elgeeko1-docker-ansible.git
- (optional, ipv6 only) docker configured for ipv6

# How to use this role
### Method 1: Install using ansible-galaxy

The most robust way to install this role is to use ansible-galaxy,
which is installed with ansible by default. ansible-galaxy is effectively a package manager for ansible. It installs roles
from the community, or from private git repos, into your local machine for use in your playbooks.

Start by adding this role to an ansible-galaxy dependency file. Typically this file lives alongside your playbook file and by convention is named `requirements.yml`.

Add the following section to `requirements.yml`:

```
roles:
  - name: elgeeko1-dnscrypt-proxy-ansible
    src: https://github.com/elgeeko1/elgeeko1-dnscrypt-proxy-ansible
    version: main
```

If there is already a `roles` section, simply append this role to
add it as a dependency.

Then, install the role using ansible-galaxy:

`ansible-galaxy install -r requirements.yml -v`

### Method 2: Clone this repository into a `roles` directory

Use this method if you plan to modify this role, or if for some
reason the ansible-galaxy method fails.

Starting from your playbook directory, change into the `roles`
directory and clone:

```
$ ls
 > playbook.yml
 > roles/
$ cd roles/
roles$ git clone https://github.com/elgeeko1/dnscrypt-proxy-ansible
```
