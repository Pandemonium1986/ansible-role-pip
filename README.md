# Ansible role : Pip

![Ansible Role](https://img.shields.io/ansible/role/39723?logo=ansible)
![Gitlab pipeline status](https://img.shields.io/gitlab/pipeline/Pandemonium1986/ansible-role-pip?logo=gitlab)
![GitHub release](https://img.shields.io/github/release/Pandemonium1986/ansible-role-pip.svg?logo=github)
![Github license](https://img.shields.io/github/license/Pandemonium1986/ansible-role-pip.svg?logo=github)
![Ansible Quality Score](https://img.shields.io/ansible/quality/39723?logo=ansible)

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
