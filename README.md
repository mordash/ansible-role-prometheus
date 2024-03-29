prometheus
==========

The present role :
  - installs prometheus server inside a Docker container
  - installs various prometheus exporter

It has been tested on :
  - Debian 9
  - Debian 10

Role variables
--------------

| Variable                                     | Type    | Choices                                                                    | Default     | Comment         |
|----------------------------------------------|---------|----------------------------------------------------------------------------|-------------|-----------------|
| prometheus_server_enable                     | string  | true / false                                                               |             |                 |
| prometheus_server_version                    | string  |                                                                            |  latest     |                 |
| prometheus_server_monitor                    | string  |                                                                            |             |                 |
| prometheus_server_global_scrape_interval     | string  |                                                                            |  15         |                 |
| prometheus_server_global_evaluation_interval | string  |                                                                            |  15         |                 |
| prometheus_server_job_name                   | string  |                                                                            |  prometheus |                 |
| prometheus_server_scrape_interval            | string  |                                                                            |  5          |                 |
| prometheus_server_scrape_timeout             | string  |                                                                            |  5          |                 |
| prometheus_exporter_packages                 | list    | node / mysqld / postgresql / mongodb / phpfpm / apache / haproxy / varnish |             |                 |
| prometheus_node_exporter_targets             | list    |                                                                            |             |                 |
| prometheus_mysqld_exporter_targets           | list    |                                                                            |             |                 |
| prometheus_mongodb_exporter_targets          | list    |                                                                            |             |                 |
| prometheus_postgres_exporter_targets         | list    |                                                                            |             |                 |
| prometheus_mysqld_exporter_user              | string  |                                                                            |             |                 |
| prometheus_mysqld_exporter_password          | string  |                                                                            |             |                 |
| prometheus_mongodb_exporter_host             | string  |                                                                            | localhost   |                 |
| prometheus_mongodb_exporter_port             | string  |                                                                            | 27017       |                 |
| prometheus_mongodb_exporter_user             | string  |                                                                            |             |                 |
| prometheus_mongodb_exporter_pass             | string  |                                                                            |             |                 |
| prometheus_server_version                    | string  |                                                                            |  latest     |                 |

Dependencies
------------

  - jq
  - Docker must installed and running for prometheus server

Example Playbook
----------------

    - hosts: prometheus
      ignore_errors: "{{ ansible_check_mode }}" # ignore errors only in check mode !

      roles:
        - { role: brainsys.prometheus, tags: ['prometheus'] }

Example variables
-----------------

    ---
    prometheus_server_enable: 'true'
    prometheus_server_monitor: 'example'

    prometheus_exporter_packages:
      - node
      - mysqld

    prometheus_mysqld_exporter_user: 'foo'
    prometheus_mysqld_exporter_password: 'bar'

    prometheus_node_exporter_targets:
      - server01
      - server02

    prometheus_mysqld_exporter_targets:
      - server01

TODO
----

License
-------

GPLv3

Author Information
------------------

Written by Ludovic Cartier <ludovic.cartier@brainsys.io>
