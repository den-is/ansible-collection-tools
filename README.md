# den_is.tools - an Ansible collection to deploy 70+ tools

An extremely minimalistic Ansible collection to quickly automate the deployment of various open-source tools and services.

A **List of available tools** can be found in the [roles](./roles/) directory and its subdirectories, such as [iaac](./roles/iaac/), [k8s](./roles/k8s/), [python](./roles/python/)

- The collection includes roles for tools that typically:
  - Require manual installation
  - Have outdated versions in OS-native package repositories
  - Are completely missing from package repositories
- **Sudo/become=true** privileges are required by default to install tools in `/usr/local/bin` or other system-wide
locations.
  - Installing in user directories does not require elevated privileges. For example, for Windows WSL install tools in
  `~/.local/bin` without `sudo/become`
  - Some roles strictly require elevated privileges, because of:
    - installing packages via package manager
    - adding repositories
    - editing system files
    - managing system services
- This collection is particularly useful and tested for **Linux x86_64** and **arm64** hosts.
  - MacOS deployments are supported, but not extensively tested.
    - You can deploy tools from archives/binaries as on a Linux host
    - Or choose to do a Homebrew deployment. TBH, in case of Homebrew deploys - you don't need to use this collection. Just
  create a task(s) yourself.
  - Microsoft Windows is unsupported - Windows WSL works just fine as a usual Linux environment
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
```

More details can be found in the official Ansible collection [docs](https://docs.ansible.com/projects/ansible/latest/collections_guide/collections_installing.html).

## Usage
Make sure that system has required packages installed or install them early in the playbook.
Required system packages: `unzip`, `bzip2`, `gnu-tar` from Homebrew on MacOS

Create a playbook, e.g. `tools-deploy.yaml`
```yaml
- name: Tools deploy
  hosts: all
  become: false
  vars:

    # many roles in the colleciton accept `tools_bin_dst` variable to set common path for all tools
    # useful if you want to install all tools, for example in `~/.local/bin`
    # by default most roles install binaries into `/usr/local/bin`
    tools_bin_dst: ~/.local/bin

    terragrunt_v: v0.95.1
    terragrunt_bin_dst: '~/test-bin-dst/should/exist'

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

More in [examples](./examples/)

### Binaries destination
By default most roles deploy downloaded binaries to `/usr/local/bin`.  
Roles such as `haproxy`, `nvm`, `pyenv`, `golang`, `ohmyzsh`, and some others, are exclusions.
Because paths for this roles are defined by specific installation instructions.

Use `tools_bin_dst` to bulk change binaries deployment destination for the most roles. For example to deploy binaries to `~/.local/bin` to avoid escalated root privileges, insted of default `/usr/local/bin`

If you set custom binary path make sure to add it to `PATH` env variable for the remote_host, so ansible's able to find binaries in the custom destination. Example:
```yaml
  # https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_environment.html#working-with-language-specific-version-managers
  environment:
    PATH: "{{ ansible_env.PATH }}:{{ ansible_env.HOME }}/.local/bin"
```
