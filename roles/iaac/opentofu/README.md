# OpenTofu

## Links
- https://opentofu.org/
- https://github.com/opentofu/opentofu

## Requirements
Requires packates `unzip` and `gnupg`

Can be deployed with a separate task in a playbook:
```yaml
- name: Install requried packages
  ansible.builtin.package:
    name: "{{ item }}"
    state: present
  become: true
  loop:
  - gnupg2
  - unzip
```
