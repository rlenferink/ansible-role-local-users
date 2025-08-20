# local_users Ansible role

This role describes local Linux user related tasks that are managed via Ansible.

## Role variables

* `local_users`: Local users that will be created (required).
* `local_groups`: Local groups that will be created (default = `[]`).
* `local_users_password_salt`: The salt to use for idempotent password generation (default = the first 16 characters of the `inventory_hostname`).

In addition to the above variables, variables ending in `__local_groups` will be merged.

See the [`defaults/main.yml`](./defaults/main.yml) for a more extensive description per variable.

## Examples

```yaml
# ansible/host_vars/node1/local-users.yml
local_users:
  podman:
    fullname: podman system user
    system: true
    lingering: true
    podman: true
    uid: 900
    subordinate_ids:
      uid: 65142784
      gid: 65142784

  root:
    fullname: root
    password: "{{ root_user_password }}"
    authorized_keys:
      - "{{ public_key1 }}"
      - "{{ public_key2 }}"
```
