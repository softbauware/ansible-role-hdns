# ansible-role-hdns [![GitHub Actions Build](https://img.shields.io/github/workflow/status/softbauware/ansible-role-hdns/ansible-lint)](https://github.com/softbauware/ansible-role-hdns/actions) [![GitHub license](https://img.shields.io/github/license/softbauware/ansible-role-hdns)](https://github.com/softbauware/ansible-role-hdns/blob/master/LICENSE)

[![Galaxy Quality Score](https://img.shields.io/ansible/quality/hdns)](https://github.com/softbauware/ansible-role-hdns)
[![Galaxy Downloads](https://img.shields.io/ansible/role/d/hdns)](https://github.com/softbauware/ansible-role-hdns)
[![Repo Size](https://img.shields.io/github/repo-size/softbauware/ansible-role-hdns.svg)](https://github.com/softbauware/ansible-role-hdns)

---

Ansible role for automatic administration of Hetzner DNS

## Requirements

The role is tested on the following operating systems:

- Debian > 9
- Ubuntu > 18.04

## Role Variables

You can always find a up to date list of all variables in [defaults/main.yml](https://github.com/softbauware/ansible-role-hdns/blob/main/defaults/main.yml) file.

```yaml
# This is the Hetzner API Token.
# You can create one here: https://dns.hetzner.com/settings/api-token
api_token: ""

# don't touch this if you don't know what you are doing
api_endpoint: "https://dns.hetzner.com/api/v1"

# this is the default ttl for all records and zones.
# The TTL in a zone defines the TTL for the SOA Entry!
ttl: 86400

# Set this to true if you want unused records to be removed on the server.
# Use with care because it will remove all zones and and records which are not in zones var.
remove_undefined: false

# This is the variable which defines the zones and records.
# You can find a example below how to set this up correctly.
zones: []
```

## Dependencies

No dependencies to other roles are used. The role only uses url module from ansible.

## Example Playbook

```yaml
---
- hosts: localhost
  connection: local # not nessesary but useful when localhost has no ssh server
  gather_facts: false
  tasks:
    - name: "execute hdns role"
      include_role:
        name: "hdns"
      vars:
        api_token: "12345"
        remove_undefined: false # be careful here, see above what this does
        ttl: 3600 # use this to overwrite the default priority
        zones:
          - name: "example.com"
            ttl: 86400 # remove this to use default priority
            records:
              - type: "NS"
                name: "@"
                value: "helium.ns.hetzner.de."
              - type: "NS"
                name: "@"
                value: "hydrogen.ns.hetzner.com."
              - type: "NS"
                name: "@"
                value: "oxygen.ns.hetzner.com."
              - type: "MX"
                name: "@"
                value: "0 mx.example.com." # note the 0 here in front. this is the mx priority
              - type: "A"
                name: "@"
                value: "134.243.112.88"
                ttl: 60 # remove this to use the default priority
              - type: "A"
                name: "www"
                value: "134.243.112.88"
```

## License

GPL 3.0+

## Author Information

SOFTBAUWARE GmbH <https://softbauware.de>
