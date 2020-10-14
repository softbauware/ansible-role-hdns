# ansible-role-hdns

Ansible role for automatic administration of Hetzner DNS

## Requirements

The role requires the following operating system versions:

- Debian > 9
- Ubuntu > 18.04

## Role Variables

tbd

## Dependencies

No dependencies to other roles available. Only standard modules are used.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
---
- name: "manage hetzner dns"
  hosts: "linux"
  gather_facts: true
  become: true
  tasks:
    - name: "use the ansible-role-hdns role"
      include_role:
        name: ansible-role-hdns
      vars:
```

## License

GPL 3.0+

## Author Information

SOFTBAUWARE GmbH<info@softbauware.de>
