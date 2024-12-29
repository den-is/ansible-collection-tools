# Oh-My-Zsh

Setups community-driven framework for managing Zsh configuration

## Links
- https://ohmyz.sh
- https://github.com/ohmyzsh/ohmyzsh
- https://github.com/ohmyzsh/ohmyzsh/wiki/Settings

## Notes
- Supports Linux systems only
- Role should be executed by a privileged user. Or a user with `sudo` access, in that case run role with `become=true`.

## Example
```yaml
- name: Oh-my-zsh setup
  hosts: lb
  roles:
  - role: ohmyzsh
    vars:
      # you can provide default set of settings at top level
      # each of these settings can be overwritten on per user basis
      omz_theme: fishy
      omz_extra_conf:
      - export EDITOR=vim
      - export VISUAL=$EDITOR

      # if you don't supply omz_users list
      # remote_user used by ansible connection is assumed - usually it is root, so root will be configured
      omz_users:
      - name: user1
        zsh_theme: robbyrussell
        zsh_extra_config:
        - alias tf="/usr/local/bin/terraform"
        - export EDITOR=vim
        - export VISUAL=$EDITOR

      # if you supply omz_users and want to configure `root` user you should supply it too
      # if you want to configure root user only you don't need omz_users list at all, just skip it
      - name: root
        zsh_theme: fishy
        omz_update_mode: disabled
```
