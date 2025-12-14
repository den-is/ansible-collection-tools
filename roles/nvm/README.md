# NVM - Node Version manager deployment role

## Links
- https://github.com/nvm-sh/nvm

## Requirements
Requires git, curl or wget, ca-certificates. Packages can by a standalone task in a playbook:
```yaml
- name: Install packages
  ansible.builtin.package:
    name: "{{ item }}"
    state: present
  become: true
  loop:
  - git
  - curl
  - wget
  - ca-certificates
```

## Usage
- https://github.com/nvm-sh/nvm?tab=readme-ov-file#usage

Example versions to install/use:
`nvm install <version>` - where `<version></version>` can be:
- `--lts`, `--lts=argon`, `'lts/*'`, `lts/argon`
- `25.2`, `24.11.1`
- `node` for latest version. etc...
