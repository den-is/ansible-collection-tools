# tealdeer - A smarter cd command

## Links
- https://github.com/ajeetdsouza/tealdeer

## Completions
By default shell completions installation is disabled `tealdeer_deploy_completions: false`.
By default various shell completions installation require `root` access.
Default path for completions:

```yaml
bash_completions_path: /usr/share/bash-completion/completions
zsh_completions_path: /usr/share/zsh/site-functions
fish_completions_path: /usr/share/fish/vendor_completions.d
```

Completions can be installed for a local user only. Provide specific path where to deploy completions. Make sure that custom destination is created, before running this role. For example set:
```yaml
bash_completions_path: ~/.local/share/bash-completion/completions
zsh_completions_path: ~/.oh-my-zsh/custom/completions
fish_completions_path: ~/.config/fish/completions
```
