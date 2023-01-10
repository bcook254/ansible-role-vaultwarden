Ansible Role: vaultwarden
=========

Installs Vaultwarden on Linux machines.

Requirements
------------

Python modules:
  - jmespath

Permission to:
  - Install dependency packages
  - Create or modify users/groups
  - Create or modify required directories

Role Variables
--------------
A non-exhuastive list of available variables is listed below, along with their default vaules. For a list of variables available for the Vaultwarden environment configuration file please see `templates/env.j2`.

    vaultwarden_url:
    vaultwarden_file:

Location of the Vaultwarden binary to be installed. __At least one of these must be defined__. `vaultwarden_url` takes precedence over `vaultwarden_file`.

    vaultwarden_url_checksum:

When using `vaultwarden_url`, an optional checksum may be given to skip downloading the file when it has not changed. This must follow the format of the [ansible.builtin.get_url module checksum parameter](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/get_url_module.html#parameter-checksum).

    vaultwarden_enable_web_vault: true

When enabled, this role will also download the patched web-vault files.

    vaultwarden_web_vault_version: 2022.12.0

The version of Vaultwarden Web Vault to be installed.

    vaultwarden_user: vaultwarden
    vaultwarden_group: vaultwarden

The user and group that will be created and Vaultwarden will run under.

    vaultwarden_daemon: vaultwarden

The name of the service used to control the Vaultwarden process.

    vaultwarden_manage_config: false

Set to true if the vaultwarden environment config file will be managed by this role.

    vaultwarden_database:

Accepts `mysql` or `postgres` which will set the appropriate DATABASE_URL in the configuration file. An empty or different value is ignored and defaults to using sqlite.

    vaultwarden_database_name: vaultwarden

If `vaultwarden_database` is set to `mysql` or `postgres` this is the name of the schema in the database. If using sqlite this will be the database filename with `.sqlite3` appended.

    vaultwarden_database_username:
    vaultwarden_database_password:

If `vaultwarden_database` is set to `mysql` or `postgres` this is the user name and password used to connect to a MySQL/MariaDB or PostgreSQL database.

    vaultwarden_database_host: 127.0.0.1
    vaultwarden_database_port: 3306 (mysql) OR 5432 (postgres)

If `vaultwarden_database` is set to `mysql` or `postgres` this is the host addresses and port used to connect to a MySQL/MariaDB or PostgreSQL database. The default port is set based on the MySQL/PostgreSQL default ports.

    vaultwarden_home_dir: /var/lib/vaultwarden
    vaultwarden_data_dir: "{{ vaultwarden_home_dirr }}/data"
    vaultwarden_web_vault_dir: "{{ vaultwarden_home_dir }}/web-vault"
    vaultwarden_bin_dir: /usr/local/bin
    vaultwarden_config_dir: /etc/vaultwarden

Default folders created for Vaultwarden binaries and data.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: bcook254.vaultwarden
           become: yes

License
-------

MIT / BSD

Author Information
------------------

This role was created by Benjamin Cook.
