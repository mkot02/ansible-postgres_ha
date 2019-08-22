# Ansible Role: postgresql_ha
Install and configure PostgreSQL9.6 server with repmgr failover cluster. 

## Requirements
None

## Role Variables
A description of the settable variables for this role. 

### Mandatory variables
These settings are mandatory only if `postgresql_ha` variable is set to `yes`.

#### Group variables
Address IP or name which can be resolved to IP of master host in repmgr cluster:
```
postgresql_ha_master: <IP>
```

#### Host variables
Node configuration in repmgr cluster:
role - master/standby
node_id - unique number in cluster
priority - 0-100
```
postgresql_ha_config:  
  role: 'standby'
  node_id: 1
  priority: 100
```

### Default variables
Proxy settings (optional):
```
http_proxy: ''
https_proxy: ''
no_proxy: ''
```

Repository location (optional):
```
postgresql_repo_url: https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

Location of PostgreSQL binary files (optional):
```
postgresql_bin_path: /usr/pgsql-9.6/bin
```

Location of PostgreSQL PGDATA directory (optional):
```
postgresql_data_dir: /var/lib/pgsql/data
```

Location of PostgreSQL log directory (optional):
```
postgresql_log_dir: /var/log/postgres
```

Force initialisation of PostgreSQL DB. If set to 'yes', PGDATA directory will be recreated (optional)
```
postgresql_init_force: no
```

User and group that are used to start PostgreSQL service (optional)
```
postgresql_user: postgres
postgresql_group: postgres
```

Name of PostgreSQL service (optional)
```
postgresql_service: postgresql-9.6.service
```

repmgr installation and configuration for PostgreSQL nodes (optional)
If set to 'yes', repmgr will be installed and confgured
If set to 'no', multiple separate PostgreSQL servers will be created
```
postgresql_ha: no
```

Location of repmgr configuration file (optional):
```
postgresql_ha_cfgfile: /etc/repmgr/9.6/repmgr.conf
```

Name of repmgr service (optional): 
```
postgresql_ha_service: repmgr96.service
```

Repmgr failover method. Possible values [manual, automatic] (optional):
```
postgresql_ha_failover: automatic
```

## Dependencies
None

## Example Playbook
```
- hosts: psql_servers
  roles:
    - mkot02.postgresql_ha
```

## License
MIT

## Author Information
Marcin Kotarba, 2019
