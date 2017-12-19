[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Build Status](https://travis-ci.org/gserlophug/ansible-role-haproxy.svg?branch=master)](https://travis-ci.org/serlophug/ansible-role-haproxy)
HAProxy
=========

The Reliable, High Performance TCP/HTTP Load Balancer. 


Role Variables
--------------
- haproxy_user: User that execute haproxy.
- haproxy_group: Group of the user that execute haproxy.
- haproxy_version: Version of HAProxy. Valid versions are: 1.5, 1.6, 1.7 and 1.8.
- haproxy_config_dir: Directory where configuration is stored.
- haproxy_log_dir: Directory where logs are stored.
- haproxy_run_dir: Directory where pid file is stored.
- haproxy_global(List\<String\>): Each element of this list is a line of the GLOBAL section in configuration file. 
- haproxy_defaults (List\<String\>): Each element of this list is a line of the DEFAULTS section in configuration file. 
- haproxy_frontend_address (String): Bind address of the frontend. Default: "*"
- haproxy_frontend_port: Frontend port for HAProxy. Default: 10000
- haproxy_servers_balance: Type of load balancer for HAProxy. Default: roundrobin
- haproxy_servers (List\<String\>): Each element of this list is a backend server.
- haproxy_basic_auth_enabled (Bool): Activate/desactivate the basic authorization.
- haproxy_userlist (List\<Dict\>): Each element of this list is a dictionary with three items:
  - type (String): type of password (insecure-password, password).
  - user (String): username.
  - password (String): password

Example Playbook
----------------
``` yaml
    - hosts: localhost
      vars: 
        haproxy_group: haproxy
        haproxy_user: haproxy
        haproxy_version: 1.7
        haproxy_global:
          - "daemon"
          - "maxconn 256"
          - "user {{ haproxy_user }}"
          - "group {{ haproxy_group }}"
        
        haproxy_frontend_port: 80
        haproxy_servers_balance: roundrobin
        haproxy_servers: 
          - "s1 172.17.0.4:80"
          - "s2 172.17.0.5:80"

      roles:
         - { role: serlophug.haproxy }
```

License
-------

Apache 2.0

