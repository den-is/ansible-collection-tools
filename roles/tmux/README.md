# tmux - terminal multiplexer

This role deploys standalone compiled tmux binaries. To install tmux from OS packages use a separate ansible task.

This role is not doing any tmux configurations just deployment. Provide tmux configurations using dedicated ansible tasks, which would deploy such configs from somewhere, your dotfiles, config templates, static files etc.

## Links
- https://github.com/tmux/tmux
- https://github.com/tmux/tmux/wiki
- https://github.com/tmux/tmux-builds
