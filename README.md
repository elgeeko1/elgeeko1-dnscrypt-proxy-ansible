# Ansible role to deploy dockerized dnscrypt-proxy
Features:
- dnscrypt-proxy preconfigured for quad9
- runs in bridged network mode (as opposed to insecure host mode)
- (optional) ipv6 enabled using variable `dnscrypt_proxy_use_ipv6: true`

## Requirements
- ansible
