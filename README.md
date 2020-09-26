Role Name
=========

This role will configure your SSH server with advanced configuration file features.

Role Variables
--------------

This role use the following variables:

| Name                                | Type/Values         | Default value               |
| ----------------------------------- | ------------------- | --------------------------- |
| ssh_port                            | Integer             | 22                          |
| ssh_permit_root_login               | String (yes/no)     | no                          |
| ssh_allowed_groups                  | List of string      | `none`                      |
| ssh_authorized_keys_folder          | String              | /etc/ssh/authorized_keys/%u |
| ssh_pubkey_authentication           | String (yes/no)     | yes                         |
| ssh_password_authentication         | String (yes/no)     | no                          |
| ssh_challegeresponse_authentication | String (yes/no)     | no                          |
| **ssh_match_group**                 | See exemples bellow | `none`                      |
| **ssh_match_user**                  | See exemples bellow | `none`                      |
| **ssh_publics_keys**                | See exemples bellow | `none`                      |


**ssh_match_group:**

| Name           | Type/Values          | Default value |
| -------------- | -------------------- | ------------- |
| name           | String               | `none`        |
| role           | String (`void`/sftp) | `none`        |
| tcp_forwarding | String (yes/no)      | no            |
| x11_forwarding | String (yes/no)      | no            |


**ssh_match_user:**

| Name           | Type/Values          | Default value |
| -------------- | -------------------- | ------------- |
| name           | String               | `none`        |
| role           | String (`void`/sftp) | `none`        |
| tcp_forwarding | String (yes/no)      | no            |
| x11_forwarding | String (yes/no)      | no            |


**ssh_publics_keys:**

| Name      | Type/Values             | Default value |
| --------- | ----------------------- | ------------- |
| account   | String                  | `none`        |
| key       | List                    | `none`        |
| key.value | String                  | `none`        |
| key.state | String (present/absent) | `none`        |

**Exemples:**


```yaml
ssh_port: 1544

ssh_allowed_groups:
  - ssh-users
  - ssh-admins
  - sftp-users

ssh_match_group:
  - name: ssh-users
  - name: ssh-admins
    tcp_forwarding: "yes"
    x11_forwarding: "yes"
  - name: sftp
    role: sftp-users

ssh_publics_keys:
  - account: nanymus
    key: 
      - value: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAt807ClfEjg6YBbtWHYKfJOr/est4wz0qOAy1Ct8fzA {nanymus MBP}
        state: present
  - account: ansible
    key: 
      - value: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAID1ACMhlGcffU4D4vAiPtLZ1YsnKZ2SdQsmeqVtlkUO/ {ansible AWX}
        state: present
      - value: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAt807ClfEjg6YBbtWHYKfJOr/est4wz0qOAy1Ct8fzA {ansible TEST}
        state: absent

```

Example Playbook
----------------

You can use this role like in the following exemple:

```yaml
    - hosts: servers
      roles:
         - {role: role-ssh, tags: ['ssh']}
```

License
-------

MIT


