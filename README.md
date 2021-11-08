# Ansible role : Pip

![Ansible Role](https://img.shields.io/ansible/role/39723?logo=ansible)
[![Molecule](https://github.com/Pandemonium1986/ansible-role-pip/actions/workflows/molecule.yml/badge.svg?branch=master)](https://github.com/Pandemonium1986/ansible-role-pip/actions/workflows/molecule.yml)
![GitHub release](https://img.shields.io/github/release/Pandemonium1986/ansible-role-pip.svg?logo=github)
![Github license](https://img.shields.io/github/license/Pandemonium1986/ansible-role-pip.svg?logo=github)
![Ansible Quality Score](https://img.shields.io/ansible/quality/39723?logo=ansible)

Install pip3, from the os package manager or from the get-pip bootstrap script. You can also install, if needed, python packages with pip3.  

## Requirements

This role is self contained and install pip3 for debian, ubuntu, linux mint, centos.  
However, it assumes that managed node is accessible with ssh and the locales are in UTF8. See [docker-debian11](https://github.com/Pandemonium1986/docker-debian11) for a example.  

## Role Variables

From defaults/main.yml:

```yaml
---
pip_install_method: "package"     # MUST be package or get-pip.
pip_install_package_update: false # In package mode, do you update pip to the latest version.
pip_packages:       []            # The python packages (optional).
pip_user:           pandemonium   # The user who installs the python packages.
pip_extra_args:     "--user"      # The arguments for pip.
```

From vars/main.yml (depends of distribution):

```yaml
---
_packages:
  - python3-devel
  - sudo
_pip_mandatory_packages:
  - setuptools
  - wheel
_pip_executable:         pip3
_package_pip:            python3-pip
_python_executable:      python3
```

## Dependencies

None.

## Example Playbook

This playbook install pip3 with get-pip bootstrap script, then install for pandemonium user the ansible, ansible-lint and molecule packages with pip3.

```yaml
---
- name:                 Converge
  hosts:                all
  vars:
    pip_install_method: get-pip
    pip_packages:
      - ansible
      - ansible-lint
      - molecule[docker]
  tasks:
    - name:             "Include ansible-role-pip"
      include_role:
        name:           "pandemonium1986.pip"
```

This playbook install pip3 with the OS package manager.

```yaml
---
- name:                 Converge
  hosts:                all
  vars:
    pip_install_method: package
    pip_packages: [ ]
  tasks:
    - name:             "Include ansible-role-pip"
      include_role:
        name:           "pandemonium1986.pip"
```

This playbook install pip3 with the OS package manager and update it with pip (Necessary for the CentOS).

```yaml
---
- name:                 Converge
  hosts:                all
  vars:
    pip_install_method: package
    pip_install_package_update: true
  tasks:
    - name:             "Include ansible-role-pip"
      include_role:
        name:           "pandemonium1986.pip"
```

## Disclaimer

-   This playbook installs python3 from the OS package manager. Then, all tasks are done with python3 excepting for `CentOS7`  
-   The latest version of python3 in `debian9` is 3.5 which is currently incompatible with get-pip. Thus, `debian9` only supports package mode.  
-   The version of pip3 installed with package mode in `debian9`, `ubuntu1804` and `mint19` has an idempotency problem. The Playbook correctly installs the pip3 and python3 packages but the github action fails during the idempotency step. To keep unit tests consistent the choice was made not to test this mode for the OS mentioned above.
- The pip version supported by the `CentOS` package manager is too old to install recent packages. If you wish, you can update pip with pip once installed with the manager package. This option is not recommended because of a consistency problem between the pip version known by the OS and the real version

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details

## Author Information

-   **Michael Maffait** - _Initial work_ - [Pandemonium1986](https://github.com/Pandemonium1986)
