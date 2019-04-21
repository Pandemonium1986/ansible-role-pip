# Ansible role : Pip

![](https://img.shields.io/github/release/Pandemonium1986/ansible-role-pip.svg)
![](https://img.shields.io/github/repo-size/Pandemonium1986/ansible-role-pip.svg)
![](https://img.shields.io/github/release-date/Pandemonium1986/ansible-role-pip.svg)
![](https://img.shields.io/github/license/Pandemonium1986/ansible-role-pip.svg)

Install and configure pip, from get-pip.py

## Requirements

This role is self contained and install pip for debian, ubuntu, linux mint, centos.

## Role Variables

From vars/main.yml (depends of distribution):

```yaml
_packages:
  - python3-dev
```

## Dependencies

None.

## Example Playbook

```yaml
- name :         Pip play
  hosts :        pandama
  become:        true
  become_method: sudo
  become_user:   root
  tasks:
    - import_role:
        name:    pandemonium1986.pip
```

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details

## Author Information

-   **Michael Maffait** - _Initial work_ - [Pandemonium1986](https://github.com/Pandemonium1986)
