# bat - A cat(1) clone with wings

## Links
- https://github.com/sharkdp/bat

## Post deploy
Run `bat cache --build` to update bat cache (to update themes and stuff)

## Completions
By default shell completions installation is disabled `tealdeer_deploy_completions: false`.
By default various shell completions installation require `root` privileges.
Default paths for completions:

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

## Manual pages
Same for deploying man pages to user dir without sudo permissions.
By default man base dir is `/usr/share/man` and requires privileged permissions to deploy in that directory.  
Set it to `~/.local/share/man` and make sure this directory exists.
