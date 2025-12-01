# chezmoi - dotfiles manager

- https://github.com/twpayne/chezmoi
- https://www.chezmoi.io

## deployment
Ansible role has artifacts deployment order. `archive` has the highest precedence if for some reason every option is `true`. Then `binary`, and finally `package`.

```yaml
chezmoi_install_archive: true
chezmoi_install_binary: false
chezmoi_install_package: false
```
