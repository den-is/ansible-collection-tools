# Oh-My-Zsh

Setups community-driven framework for managing Zsh configuration

## Links
- https://ohmyz.sh/
- https://github.com/ohmyzsh/ohmyzsh
- https://github.com/ohmyzsh/ohmyzsh/wiki/Settings

## Notes
- Role should be installed using root user if you pass a list of user
  - or supply `become=true` during the role call
  - in that case user should have sudo privilege
- tested and works mainly with Linux systems
  - MacOS/Darwin should be moved in own play/tasks, and usually you don't want such a rudementary .zshrc setup for your MacOS

## Example
```yaml
- name: Oh-my-zsh setup
  hosts: lb
  roles:
  - role: ohmyzsh
    vars:
      # you can provide default set of settings at top level
      # each of these settings can be overwritten on per user basis
      zsh_theme: fishy
      zsh_extra_config:
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
