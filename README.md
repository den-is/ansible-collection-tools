# den_is.tools - Ansible collection

⚠️ Under development. 👷

This Ansible collection automates the installation of various tools, services and environments.  
Roles in this collection are extremely minimalistic and at some places ugly, there are no tests.
It may lack some features compared to more comprehensive roles/collections. Make sure to check all options.

But for me it works well enough, if I can quickly install tool X, tool Y and ohmyzsh on some random Linux box for my convinience without visiting each tool's Installation doc page.

- Collection includes roles for tools which typically:
  - Require manual installation
  - OS-native package repositories have outdated versions
  - or completely missing desired package
- This collection is particularly useful for Linux hosts
- Linux hosts are the primary target for this collection, followed by macOS
- Windows is unsupported

Contributions are welcome.

## Available tools
```sh
├── age
├── awscli
├── bat
├── cfssl
├── croc
├── direnv
├── eza
├── fd
├── fzf
├── git_delta
├── haproxy
├── iaac
│   ├── atlantis
│   ├── opentofu
│   ├── packer
│   ├── terraform
│   ├── terragrunt
│   ├── terragrunt_atlantis_config
│   └── vagrant
├── k8s
│   ├── argocd
│   ├── flux
│   ├── helm
│   ├── helmfile
│   ├── k3d
│   ├── k9s
│   ├── kind
│   ├── kubecolor
│   ├── kubectl
│   ├── kubectx
│   ├── kubefwd
│   ├── kubeps1
│   ├── kubeseal
│   ├── kubie
│   ├── kustomize
│   ├── stern
│   └── talosctl
├── lazydocker
├── lazygit
├── minio
├── mkcert
├── neovim
├── ohmyzsh
├── pyenv
├── rclone
├── restic
├── ripgrep
├── sops
├── syncthing
├── yq
├── zellij
└── zoxide
```

## Installation

```sh
# Installing from galaxy
ansible-galaxy collection install den_is.tools

# Local dev installation
# By default installs into ~/.ansible/collections/ansible_collections/den_is/tools
ansible-galaxy collection install ~/projects/ansible_collections/den_is/tools
ansible-galaxy collection install ~/projects/ansible_collections/den_is/tools --upgrade

ansible-galaxy collection build
ansible-galaxy collection install den_is-tools-0.18.0.tar.gz -p ./collections

ansible-galaxy collection install git+https://github.com/den-is/ansible-collection-tools.git
```

## Usage
- Install collection using one of the methods listed above or in [Ansible Collections](https://docs.ansible.com/ansible/latest/collections_guide/collections_installing.html) doc
- Create playbook
  ```yaml
  ---
  - name: Install common tools
    hosts: all
    become: false
    environment:
      PATH: "/home/den/.local/bin:{{ ansible_env.PATH }}"
    vars:
      # set top-level playbook variables
      terragrunt_v: v0.58.12
      terragrunt_bin_dst: ~/.local/bin

    tasks:

    - name: Install terragrunt in user's home
      ansible.builtin.import_role:
        name: den_is.tools.iaac.terragrunt
      tags: tg

    - name: Install OpenTofu in user's home
      ansible.builtin.import_role:
        name: den_is.tools.iaac.opentofu
      vars:
        # set role import variables
        opentofu_v: v1.7.1
        opentofu_bin_dst: ~/.local/bin
      tags: tofu

    - name: Install helm globally using role defaults
      ansible.builtin.import_role:
        name: den_is.tools.k8s.helm
      become: true
      tags: helm
  ```
- Run ansible-playbook providing hosts inventory using one of the many methods:
  ```sh
  ansible-playbook -i '<my-host-ip>,' common-tools-setup.yaml
  ```
