# Setting up Fedora environment

```sh
# Install den_is.tools ansible collection
ansible-galaxy collection install den_is.tools
# or
ansible-galaxy install -r requirements.yaml

# First run playbook dedicated for root to setup global settings and packages
ansible-playbook -i <host-ip>, playbooks/root.yaml --ask-become-pass

# Then run playbook for user to setup user specific tasks
ansible-playbook -i <host-ip>, playbooks/user.yaml --ask-become-pass

# To upgrade collection. One of the methods:
ansible-galaxy collection install den_is.tools --upgrade
```
