# Ansible Role: Common

---

## Requirements

None.

## Example Playbook

```yaml
- hosts: all
  vars:
    # group_vars
    ssh_permit_root_login: yes
    selinux_state: disabled
    
    # Downloading pub key location (for deploy user)
    fetch_private_dir: ./.private/{{ inventory_hostname }}

    deploy_user_name: deploy
    deploy_user_pass: '$6$JH.YZ3IgJDAIHXs$aX9tBAlbJX6KEaLI6WFMpWXfri8RK4H3/'
    deploy_user_public_keys:
      - ~/.ssh/id_rsa.pub
    groups_add:
      - developers
    users_add:
      - name: username
        password: '$6$JH.YZ3IgJDAIHXs$aX9tBAlbJX6KEaLI6WFMpWXfri8RK4H3/'
        groups: wheel, developers
        create_home: no
    
    repo_install:
      - url: https://archive.fedoraproject.org/pub/epel/epel-release-latest-{{ ansible_distribution_major_version }}.noarch.rpm
        gpg_key: https://archive.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-{{ ansible_distribution_major_version }}    
    
    install_gen_packages: []
    install_ext_packages: []
        
    #host_vars
    server_name: node1-db
  roles:
    - cinject.common
```

## License

MIT / BSD