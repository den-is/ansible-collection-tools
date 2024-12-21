# Go - Golang programming language setup

Role installs Golang system-wide.  
Because of that role should be run as root or `become=true`

By default Go sets `$GOPATH` as `$HOME/go` [doc1](https://go.dev/wiki/GOPATH), [doc2](https://go.dev/wiki/SettingGOPATH).  
Users should not forget to add `$GOPATH/bin` to their .bashrc, .zshrc or other alternatives including system wide configurations for example. `/etc/profile.d/`

- [Official Golang website](https://go.dev)
