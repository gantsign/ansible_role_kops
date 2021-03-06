Ansible Role: kops
==================

[![Build Status](https://travis-ci.com/gantsign/ansible_role_kops.svg?branch=master)](https://travis-ci.com/gantsign/ansible_role_kops)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gantsign.kops-blue.svg)](https://galaxy.ansible.com/gantsign/kops)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gantsign/ansible_role_kops/master/LICENSE)

Role to download and install [kops](https://github.com/kubernetes/kops) the tool
for getting production grade Kubernetes clusters up and running.

Requirements
------------

* Ansible >= 2.8

* Linux Distribution

    * Debian Family

        * Debian

            * Jessie (8)
            * Stretch (9)

        * Ubuntu

            * Xenial (16.04)
            * Bionic (18.04)

    * RedHat Family

        * CentOS

            * 7

    * Note: other versions are likely to work but have not been tested.

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# kops version number
kops_version: 'v1.18.2'

# Mirror to download the kops from
kops_mirror: 'https://github.com/kubernetes/kops/releases/download/{{ kops_version }}'

# Directory to store files downloaded for kops
kops_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: gantsign.kops
```

Tab Completion for Zsh
----------------------

### Using Ansible

We recommend using the
[gantsign.antigen](https://galaxy.ansible.com/gantsign/antigen) role to enable
tab completion for kops (this must be configured for each user).

```yaml
- hosts: servers
  roles:
    - role: gantsign.kops

    - role: gantsign.antigen
      users:
        - username: example
          antigen_libraries:
            - name: oh-my-zsh
          antigen_bundles:
            - name: kops
```

### Using Antigen

If you prefer to use [Antigen](https://github.com/zsh-users/antigen) directly
add the following to your Antigen configuration:

```bash
antigen bundle kops
```

### Manual configuration

To manually configure Zsh add the following to your `.zshrc`:

```bash
eval "$(kops completion zsh)"
```

More Roles From GantSign
------------------------

You can find more roles from GantSign on
[Ansible Galaxy](https://galaxy.ansible.com/gantsign).

Development & Testing
---------------------

This project uses [Molecule](http://molecule.readthedocs.io/) to aid in the
development and testing; the role is unit tested using
[Testinfra](http://testinfra.readthedocs.io/) and
[pytest](http://docs.pytest.org/).

To develop or test you'll need to have installed the following:

* Linux (e.g. [Ubuntu](http://www.ubuntu.com/))
* [Docker](https://www.docker.com/)
* [Python](https://www.python.org/) (including python-pip)
* [Ansible](https://www.ansible.com/)
* [Molecule](http://molecule.readthedocs.io/)

Because the above can be tricky to install, this project includes
[Molecule Wrapper](https://github.com/gantsign/molecule-wrapper). Molecule
Wrapper is a shell script that installs Molecule and it's dependencies (apart
from Linux) and then executes Molecule with the command you pass it.

To test this role using Molecule Wrapper run the following command from the
project root:

```bash
./moleculew test
```

Note: some of the dependencies need `sudo` permission to install.

License
-------

MIT

Author Information
------------------

John Freeman

GantSign Ltd.
Company No. 06109112 (registered in England)
