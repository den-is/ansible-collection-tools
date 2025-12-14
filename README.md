# den_is.tools - an Ansible collection

An extremely minimalistic Ansible collection to quickly automate the deployment of various open-source tools and services.

A **List of available tools** can be found in the [roles](./roles/) directory and its subdirectories, such as [iaac](./roles/iaac/), [k8s](./roles/k8s/), [python](./roles/python/)

- The collection includes roles for tools that typically:
  - Require manual installation
  - Have outdated versions in OS-native package repositories
  - Are completely missing from package repositories
- Most tools are installed by default into `/usr/local/bin`, but can also be installed into `~/.local/bin` or any custom location
- Some roles require a `sudo|become` password, especially when deploying globally or when system packages are required
  - Other roles do not require `sudo`, particularly when deploying into local/user directories
- This collection is particularly useful and tested for Linux x86_64 and arm64 hosts
  - MacOS deployments are supported by not extensively tested. First method to deploy on MacOS is `Homebrew`, then plain `binaries` can be deployed too if you indicate proper paths.
  - Microsoft Windows is unsupported
- 99% of the roles in this collection perform only binary downloads and deployments:
  - Extra configuration, rc files, dotfiles, etc. are handled outside of these roles using dedicated tasks or playbooks

No warranties are provided whatsoever.  
All credit for the tools included in this collection goes to the tools’ authors and contributors.  

In contrast to some brilliant roles and collections on the internet, this collection and its roles are not super polished, do not include tests, and do not always cover all possible deployment cases. I don’t care. I’ve used this collection for several years, and it has helped me many times to extremely quickly kickstart random Linux environments from scratch.

## Contributions are more than welcome
If you like this collection, something does not work, or you want add a tool - open an [Issue](https://github.com/den-is/ansible-collection-tools/issues) or a PR. Just follow more or less the same format as existing roles here.

## Installation

```sh
# Install latest from galaxy
ansible-galaxy collection install den_is.tools

# Install latest from git
ansible-galaxy collection install git+https://github.com/den-is/ansible-collection-tools.git

# Local dev installation
# By default installs into ~/.ansible/collections/ansible_collections/den_is/tools
git clone https://github.com/den-is/ansible-collection-tools.git
ansible-galaxy collection install ./ansible-collection-tools
ansible-galaxy collection install ./ansible-collection-tools --upgrade

# build and install from archive
ansible-galaxy collection build
ansible-galaxy collection install den_is-tools-0.50.0.tar.gz -p ./collections
```

More details can be found in the official Ansible collection [docs](https://docs.ansible.com/projects/ansible/latest/collections_guide/collections_installing.html).

## Usage

Create a playbook, e.g. `tools-deploy.yaml`
```yaml
- name: Tools deploy
  hosts: all
  become: false
  environment:
    PATH: "{{ ansible_env.HOME }}/.local/bin:{{ ansible_env.PATH }}"
  vars:
    # set top-level playbook variables
    common_bin_dst: ~/.local/bin

    terragrunt_v: v0.95.1
    terragrunt_bin_dst: '{{ common_bin_dst }}'

  tasks:

  # requires elevated privileges
  - name: Install helm globally using role defaults
    ansible.builtin.import_role:
      name: den_is.tools.k8s.helm
    become: true

  # does not require elevated privileges
  - name: Install terragrunt in user's home
    ansible.builtin.import_role:
      # custom vars are set above
      name: den_is.tools.iaac.terragrunt

  # does not require elevated privileges
  - name: Install specific OpenTofu version in user's home
    ansible.builtin.import_role:
      name: den_is.tools.iaac.opentofu
    vars:
      # set role variables "inline"
      opentofu_v: v1.11.1
      opentofu_bin_dst: ~/.local/bin
```

Run `ansible-playbook` providing hosts inventory using one of the many supported methods:

```sh
ansible-playbook -i '<my-host-ip>,' tools-deploy.yaml
# or if you installing globally and need sudo/root access
ansible-playbook -i '<my-host-ip>,' tools-deploy.yaml --ask-become-pass
```
