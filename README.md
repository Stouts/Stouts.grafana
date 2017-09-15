Stouts.grafana
==============

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.grafana.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.grafana)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.grafana-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/1907)

Ansible role which manage [Grafana](http://http://grafana.org/)

* Install and configure Grafana


#### Variables

Here is the list of all variables and their default values:

```yaml
grafana_enabled: true                       # The role is enabled
grafana_apt_repository: deb https://packagecloud.io/grafana/stable/debian/ jessie main
grafana_apt_key: https://packagecloud.io/gpg.key

grafana_version: 3.1.1-*                    # Set version (set to latest to install latest version)

grafana_app_mode: production

# Paths
grafana_data: /var/lib/grafana
grafana_logs: /var/log/grafana
grafana_plugins: "{{ grafana_data }}/plugins"
grafana_plugins_install: []

# Server
grafana_protocol: http
grafana_http_addr: 0.0.0.0                  # The ip address to bind to
grafana_http_port: 3000                     # The http port  to use
grafana_domain: localhost                   # The public facing domain name used to access grafana from a browser
grafana_api_base_url: "http://{{ grafana_domain }}"
grafana_enforce_domain: false
grafana_root_url: "%(protocol)s://%(domain)s:%(http_port)s/"
grafana_router_logging: false                  # Log web requests
grafana_static_root_path: public            # the path relative working path
grafana_enable_gzip: false                     # enable gzip
grafana_cert_file:                          # https certs & key file
grafana_cert_key:

# Database
grafana_type: sqlite3                       # Either "mysql", "postgres" or "sqlite3"
grafana_host: 127.0.0.1:3306
grafana_name: grafana
grafana_user: root
grafana_password:
grafana_ssl_mode: disable                   # For "postgres" only, either "disable", "require" or "verify-full"
grafana_path: grafana.db                    # For "sqlite3" only, path relative to data_path setting

# Session
grafana_provider: file                      # Either "memory", "file", "redis", "mysql", default is "memory"
grafana_provider_config: sessions
grafana_cookie_name: grafana_sess           # Session cookie name
grafana_cookie_secure: false                # If you use session in https only
grafana_session_life_time: 86400            # Session life time, default is 86400

# Analytics
grafana_reporting_enabled: true             # Server reporting, sends usage counters to stats.grafana.org every 24 hours.
grafana_check_for_updates: true             # Set to false to disable all checks to https://grafana.net
grafana_google_analytics_ua_id:             # Google Analytics universal tracking code, only enabled if you specify an id here

# Security
grafana_admin_user: admin                   # Default admin username
grafana_admin_password: admin               # Default admin password
grafana_secret_key: ECaamBjja2CChzAp        # Used for signing
grafana_login_remember_days: 7
grafana_cookie_username: grafana_user
grafana_cookie_remember_name: grafana_remember
grafana_disable_gravatar: false                # disable gravatar profile images
grafana_data_source_proxy_whitelist:        # data source proxy whitelist (ip_or_domain:port seperated by spaces)

# Snapshots
grafana_external_enabled: true
grafana_external_snapshot_url: https://snapshots-origin.raintank.io
grafana_external_snapshot_name: Publish to snapshot.raintank.io

# Users
grafana_allow_sign_up: true                 # Disable user signup/registration
grafana_allow_org_create: true              # Allow falsen admin users to create organizations
grafana_auto_assign_org: true               # Set to true to automatically assign new users to the default organization (id 1)
grafana_auto_assign_org_role: Viewer        # Default role new users will be automatically assigned
grafana_login_hint: email or username       # Background text for the user field on the login page

# Anonymous Auth
grafana_anonymous_enabled: false               # Enable Anonymous access
grafana_anonymous_org_name: Main Org.       # Specify organization name that should be used for unauthenticated users
grafana_anonymous_org_role: Viewer          # Specify role for unauthenticated users

# Github Auth
grafana_github_enabled: false                  # Enable Github Auth
grafana_github_client_id: some_id
grafana_github_client_secret: some_secret
grafana_github_scopes: user:email
grafana_github_auth_url: https://github.com/login/oauth/authorize
grafana_github_token_url: https://github.com/login/oauth/access_token
grafana_github_api_url: https://api.github.com/user
grafana_github_team_ids:
grafana_github_allowed_organizations:
grafana_github_auth_allow_sign_up: true

# Google Auth
grafana_google_enabled: false                  # Enable Google Auth
grafana_google_client_id: some_id
grafana_google_client_secret: some_secret
grafana_google_scopes: https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email
grafana_google_auth_url: https://accounts.google.com/o/oauth2/auth
grafana_google_token_url: https://accounts.google.com/o/oauth2/token
grafana_google_api_url: https://www.googleapis.com/oauth2/v1/userinfo
grafana_google_allowed_domains: mycompany.com othercompany.com
grafana_google_auth_allow_sign_up: true

# Basic Auth
grafana_auth_basic_enabled: true

# Auth Proxy
grafana_auth_proxy_enabled: false
grafana_auth_proxy_header_name: X-WEBAUTH-USER
grafana_auth_proxy_header_property: username
grafana_auth_proxy_auto_sign_up: true

# Auth LDAP
grafana_auth_ldap_enabled: false
grafana_auth_ldap_config_file: /etc/grafana/ldap.toml

# SMTP / Emailing
grafana_smtp_enabled: false
grafana_smtp_host: localhost:25
grafana_smtp_user:
grafana_smtp_password:
grafana_smtp_cert_file:
grafana_smtp_key_file:
grafana_smtp_skip_verify: false
grafana_smtp_from_address: admin@grafana.localhost
grafana_emails_welcome_email_on_sign_up: false

# Logging
grafana_log_mode: console, file
grafana_log_buffer_len: 10000
grafana_log_level: Info

# AMPQ Event Publisher
grafana_ampq_enabled: false
grafana_ampq_rabbitmq_url: amqp://localhost/
grafana_ampq_exchange: grafana_events

# Dashboard JSON files
grafana_dashboard_json_enabled: false
grafana_dashboard_json_path: /var/lib/grafana/dashboards

# Setup nginx configuration
grafana_nginx: false
grafana_nginx_servername: "{{inventory_hostname}}"
grafana_nginx_ssl: false
grafana_nginx_ssl_crt: ""
grafana_nginx_ssl_key: ""
grafana_nginx_ssl_redirect: "{{grafana_nginx_ssl}}"
grafana_nginx_port: 80

# Grafana users (add using api)
grafana_users: []                              # list of dict with format: {username: 'user1', password: 'pass1'}

```

#### Usage

Add `Stouts.grafana` to your roles and setup the variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.grafana

  vars:
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.grafana/issues)!

If you wish to express your appreciation for the role, you are welcome to send
a postcard to:

    Kirill Klenov
    pos. Severny 8-3
    MO, Istra, 143500
    Russia
