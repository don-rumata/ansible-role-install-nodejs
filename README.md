# Ansible Role: Install NodeJS

[![License][license-image]][license-url] [![Ansible Galaxy][ansible-galaxy-image]][ansible-galaxy-url] [![CircleCI][circleci-image]][circleci-url]

Install [nodejs](https://nodejs.org/) for Linux and Windows.

## Work on

### Ansible Galaxy style

```yaml  platforms:
    - name: Fedora
      versions:
        - 28
        - 29
        - 30
        - 31
        - 32
    - name: Ubuntu
      versions:
        - trusty
        - xenial
        - bionic
        - cosmic
        - disco
        - eoan
        - focal
    - name: Debian
      version:
        - jessie
        - stretch
        - buster
        - sid
    # https://github.com/ansible/galaxy/issues/2072
    - name: EL
      versions:
        - 7
        - 8
    - name: opensuse
      vesrion:
        - tumbleweed
        - 15.1
        - 15.2
    - name: Windows
      version:
        - 2008x64 (7 64bit)
        - 2008x86 (7 32bit)
        - 2019 (10 64bit)
```

## Requirements

[min_ansible_version: 2.8](https://docs.ansible.com/ansible/latest/modules/snap_module.html)

## Role Variables

```yaml
#--- NodeJS method install ---#
nodejs_method_install: package-manager
# nodejs_method_install: snap

#--- Version section ---#
nodejs_major_version: 'lts'
# nodejs_major_version: 'current'
# nodejs_major_version: 14
# nodejs_major_version: 12
# nodejs_major_version: 10

#--- Snap section ---#
ansible_role_for_install_snap: don_rumata.ansible_role_install_snap

#--- Proxy section ---#
nodejs_use_over_proxy: false
# nodejs_use_over_proxy: true
nodejs_proxy_host: proxy.example.com
nodejs_proxy_port: 3128
nodejs_proxy_string: http://{{ nodejs_proxy_host }}:{{ nodejs_proxy_port }}

#--- Repo section ---#
nodejs_index_json_url: https://nodejs.org/dist/index.json
nodejs_repo_deb_key: https://deb.nodesource.com/gpgkey/nodesource.gpg.key
nodejs_repo_rpm_key: https://rpm.nodesource.com/pub/el/NODESOURCE-GPG-SIGNING-KEY-EL

# https://nodejs.org/dist/v12.18.2/SHASUMS256.txt
nodejs_checksum_algorithm: sha256

#--- Local paths section ---#
nodejs_windows_local_download_path: '{{ ansible_env.TMP }}\nodejs'

# If you *NOT* use apt-cacher-ng or other caching proxy - select "https".
http_or_https: http
# http_or_https: https
```

## Dependencies

### If you want deploy to Windows 7

Download and install [Windows Management Framework 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

## HowTo

Quick config WinRM for Windows: <https://ru.stackoverflow.com/a/949971/191416>

## Example Playbook

Install latest LTS nodejs on Windows or Linux over package manager of you distro:

`install-nodejs.yml`:

```yaml
- name: Install NodeJS
  hosts: all
  strategy: free
  serial:
    - "100%"
  roles:
    - ansible-role-install-nodejs
  tasks:
```

## License

Apache License, Version 2.0

## Author Information

[don Rumata](https://github.com/don-rumata)

## TODO

- Add tests.
- Add installation support for a specific full version as `12.18.2`.

[license-image]: https://img.shields.io/github/license/don-rumata/ansible-role-install-nodejs.svg
[license-url]: https://opensource.org/licenses/Apache-2.0

[ansible-galaxy-image]: https://img.shields.io/badge/ansible_galaxy-don__rumata.ansible__role__install__nodejs-blue.svg
[ansible-galaxy-url]: https://galaxy.ansible.com/don_rumata/ansible_role_install_nodejs

[circleci-image]: https://circleci.com/gh/don-rumata/ansible-role-install-nodejs.svg?style=shield
[circleci-url]: https://circleci.com/gh/don-rumata/ansible-role-install-nodejs
