# Ansible role : Pip

[![Ansible Role](https://img.shields.io/ansible/role/d/pandemonium1986/init?logo=Ansible&color=blue)](https://galaxy.ansible.com/ui/standalone/roles/pandemonium1986/pip/)
[![Molecule](https://github.com/Pandemonium1986/ansible-role-init/actions/workflows/molecule.yml/badge.svg)](https://github.com/Pandemonium1986/ansible-role-pip/actions/workflows/molecule.yml)
![GitHub release](https://img.shields.io/github/release/Pandemonium1986/ansible-role-pip.svg?logo=github)
![Github license](https://img.shields.io/github/license/Pandemonium1986/ansible-role-pip.svg?logo=github)

Depending on your operating system, install pip or pipx from the OS package manager or from get-pip. Then install python applications from pip or pipx.

## Pip/Pix installation methods

| OS         | Method  | Pip or Pipx |
| :--------- | :------ | :---------- |
| centos7    | get-pip | pip         |
| debian12   | package | pipx        |
| ubuntu2204 | package | pipx        |
| sles15sp3  | get-pip | pip         |
| sles15sp5  | package | pipx        |
| tumbleweed | package | pipx        |

## Requirements

This role is self contained and install pip3 or pipx for debian, ubuntu, opensuse, sles, centos.  
However, it assumes that managed node is accessible with ssh and the locales are in UTF8. See [docker-debian11](https://github.com/Pandemonium1986/docker-debian11) for a example.

## Role Variables

From defaults/main.yml:

```yaml
---
pip_install_package_update: false # In package mode, do you update pip to the latest version.
pip_packages: [] # The python packages (optional).
pip_user: pandemonium # The user who installs the python packages.
pip_extra_args: "--user" # The arguments for pip (when method is get-pip).
```

From vars/[distro|familly]-[os_familly]-[os_version].yml (depends of distribution):

```yaml
---
_packages:
  - libffi-dev
  - python3-dev
  - python3-venv
  - sudo
_packages_pip:
  - python3-pip
  - pipx
_pip_executable: pipx
_pip_mandatory_packages: []
_python_executable: python3
```

## Dependencies

None.

## Example Playbook

```yaml
---
- name: Converge
  hosts: all
  vars:
    pip_user: pandemonium
    pip_packages:
      - ansible-core
      - ansible-lint
      - molecule
      - molecule-plugins[docker]
  tasks:
    - name: "Include ansible-role-pip"
      include_role:
        name: "pandemonium1986.pip"
```

```yaml
---
- name: Converge
  hosts: all
  vars:
    pip_install_method: package
    pip_install_package_update: true
  tasks:
    - name: "Include ansible-role-pip"
      include_role:
        name: "pandemonium1986.pip"
```

## Disclaimer

- This playbook installs python3 from the OS package manager. Then, all tasks are done with python3 excepting for `CentOS7`
- The Pipx package is not available for centos7 and sles15sp3. Pip is installed via get-pip for both bones. But there's nothing to stop you installing pipx and then install python applications AFTER the playbook has been run.

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details

## Author Information

- **Michael Maffait** - _Initial work_ - [Pandemonium1986](https://github.com/Pandemonium1986)
