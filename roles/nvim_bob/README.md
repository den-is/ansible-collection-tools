# Bob - Neovim installer and versions manager

## Links
- https://github.com/MordechaiHadad/bob

## Requirements
Requires `unzip` package to be available. Make sure to install it before deploying `bob`, example task:
```yaml
- name: Install unzip
  ansible.builtin.package:
    name: unzip
    state: present
  become: true
```

## Deploying neovim configuration
Warning: Often fully-fledged Neovim configuration would require extra software deployed in the environment that is not managed by this role

Probably better to deploy configuration as a separate task, outside of this role

To deploy neovim configuration using this role:

```yaml
  tasks:
  - name: Install bob neovim installer
    ansible.builtin.import_role:
      name: den_is.tools.nvim_bob
    become: true # required to install bob binary in /usr/local/bin and `unzip`
    vars:
      neovim_config_deploy: true
      neovim_config_repo: https://github.com/den-is/nvim
      # Optional
      # neovim_config_ref: HEAD
      # neovim_config_dst: ~/.config/nvim
```
