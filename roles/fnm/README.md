# fnm - Fast Node Manager

## Links
- https://github.com/Schniz/fnm

## Requirements
Target host needs `unzip` (release assets are zip archives) and `curl`/`ca-certificates` for downloads on the managed host.

Supported platforms: Linux `x86_64`, Linux `aarch64`, macOS `x86_64`/`arm64`. Linux `arm32` is not supported by the role. Linux asset is glibc-linked.

## Shell integration
The role only deploys the binary. Enable fnm in your shell profile, for example:
```sh
eval "$(fnm env --use-on-cd --shell zsh)"
```
https://github.com/Schniz/fnm?tab=readme-ov-file#shell-setup

## Node.js management
Set `fnm_manage_node: true` to install `fnm_node_version` after deploying fnm.
Accepted values are anything `fnm install` takes: `--lts`, `--latest`, `22`, `22.12.0`, `lts/iron`.
The `default` alias is set only for explicit versions, not for `--lts` and `--latest` flags.
