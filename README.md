Stouts.grafana
==============

[![Build Status](https://travis-ci.org/Stouts/Stouts.grafana.png)](https://travis-ci.org/Stouts/Stouts.grafana)

Ansible role which manage [Grafana](http://http://grafana.org/)

* Install and configure Grafana
* Setup a Grafana proxy with nginx (supports http auth)


#### Variables

Here is the list of all variables and their default values:

```yaml
grafana_enabled: yes                        # The role is enabled
grafana_version: 1.8.1                      # Set version

grafana_user: grafana
grafana_group: "{{grafana_user}}"

grafana_home: /var/lib/grafana

grafana_index: grafana-dash

grafana_datasources: []                     # Setup datasources
                                            # Example:
                                            # grafana_datasources:
                                            #   graphite:
                                            #     type: 'graphite'
                                            #     url: "http://my.graphite.server.com:8080"
                                            #   elasticsearch:
                                            #     type: 'elasticsearch'
                                            #     url: "http://my.elastic.server.com:9200"
                                            #     index: "grafana-dash"
                                            #     grafanaDB: true
# Global configuration options
grafana_max_results: 20                     # Specify the limit for dashboard search results
grafana_default_route: /dashboard/file/default.json # Default home dashboard
grafana_unsaved_changes_warning: yes        # Set to no to disable unsaved changes warning
grafana_playlist_timespan: 1m               # Set the default timespan for the playlist feature
grafana_admin_password: ""                  # Specify password before saving (this password is not security)
grafana_window_title_prefix: grafana -      # Set window title prefix
grafana_plugins_panels: []                  # List of plugin panels
grafana_plugins_dependencies: []            # Requirejs modules in plugins folder that should be loaded

grafana_proxy_nginx: yes                    # Serve Grafana with Nginx
grafana_proxy_port: 80
grafana_proxy_hostname: "{{inventory_hostname}}"  # Set hostname
grafana_proxy_log: /var/log/grafana.log
grafana_proxy_auth: no                      # Enable Basic HTTP Authentication
grafana_proxy_auth_users: []                # Setup users for the HTTP Auth
                                            # grafana_proxy_auth_users:
                                            # - { name: team, password: secret }
```

#### Usage

Add `Stouts.grafana` to your roles and setup the variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.nginx
    - Stouts.elasticsearch
    - Stouts.grafana

  vars:
    grafana_proxy_auth: yes
    grafana_proxy_auth_users:
    - name: admin
      password: iamaboss
    grafana_datasources:
      graphite:
        type: 'graphite'
        url: "http://localhost:8080"
      elasticsearch:
        type: "elasticsearch"
        url: "http://localhost:9200"
        index: "grafanaDash"
        grafanaDb: yes
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.grafana/issues)!
