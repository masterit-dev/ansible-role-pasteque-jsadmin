# Pasteque JSAdmin

An ansible role for pasteque JSAdmin interface deployment.

## Requirements

### On the node

This role requires you have a WEB server (with `Apache` or `NGINX`) running on your server along with `git`.

`PHP` is not required.

You can install the required components with [geerlingguy](https://galaxy.ansible.com/geerlingguy/) roles collections :
- `geerlingguy.apache`
- `geerlingguy.git`

## Role Variables

Main available variables are listed below, along with default values (see [defaults/main.yml](defaults/main.yml)`):

The URL of the APP (Not needed in this role but it's a helper for other role to be configured like `apache` and its vhosts):

```yaml
pasteque_jsadmin_url: "admin.pasteque.{{ domain | d(example.com) }}"
```

The root directory for the files:

```yaml
pasteque_jsadmin_dir: "/var/www/pasteque_jsadmin"
```

The URL of the repo (default is setted to pasteque official repo):

```yaml
pasteque_api_git_repo: "https://framagit.org/pasteque/pasteque-jsadmin.git"
```

## Examples Playbooks

If you have met all the requirements, this playbook should be enough:

```yaml
- hosts: all
  become: yes
  roles:
     - role: masterit_dev.pasteque_jsadmin
```

For a from-scratch installation, you can begin with this complete playbook:

```yaml
- hosts: all
  become: true
  vars:
    pasteque_jsadmin_url: admin.pasteque.example.com
    pasteque_jsadmin_dir: /var/www/pasteque_jsadmin
    apache_vhosts_filename: pasteque_jsadmin.conf
    apache_vhosts:
      - servername: "{{ pasteque_jsadmin_url }}"
        documentroot: "{{ pasteque_jsadmin_dir }}"
  roles:
    - role: geerlingguy.apache
    - role: geerlingguy.git
    - role: masterit_dev.pasteque_jsadmin
```

It will be preferable to convert all the playbook variables into `group_vars` variables.

## License

[CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/)

## Author Information

This role was created in 2021 for [Pasteque](https://www.pasteque.org) by Lucien DURAND-HARDY from [MasterIT](http://www.masterit.fr).
