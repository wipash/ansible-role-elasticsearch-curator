# Ansible Role: Elasticsearch Curator

[![Build Status](https://travis-ci.org/wipash/ansible-role-elasticsearch-curator.svg?branch=master)](https://travis-ci.org/wipash/ansible-role-elasticsearch-curator)

An Ansible Role that installs [Elasticsearch Curator](https://github.com/elasticsearch/curator) on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None, but it's a lot more helpful if you have Elasticsearch running somewhere :)

On RedHat/CentOS, make sure you have the EPEL repository configured, so the `python-pip` package can be installed. You can install the EPEL repo by simply adding `geerlingguy.repo-epel` to your playbook's roles.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticsearch_curator_version: 5.4.1
    elasticsearch_curator_hosts: 127.0.0.1
    elasticsearch_curator_port: 9200
    elasticsearch_curator_master_only: False
    elasticsearch_curator_ssl: False
    elasticsearch_curator_url_prefix:
    elasticsearch_curator_certificate:
    elasticsearch_curator_client_cert:
    elasticsearch_curator_client_key:
    elasticsearch_curator_ssl_no_validate: False
    elasticsearch_curator_timeout: 30
    elasticsearch_curator_aws_key:
    elasticsearch_curator_aws_secret_key:
    elasticsearch_curator_aws_region:
    elasticsearch_curator_aws_sign_request: False
    elasticsearch_curator_http_auth:

    elasticsearch_curator_cron_jobs:
      - {
        name: "elasticsearch_curator",
        job: "curator --config /etc/curator/config.yml /etc/curator/actions.yml",
        minute: 5,
        hour: 0
      }

    elasticsearch_curator_prefixes:
      - {
        prefix: "logstash-",
        days_to_delete: 90,
        days_to_close: 90
      }


Creates a list of actions for curator to use to prune, optimize, close, and otherwise maintain your Elasticsearch indexes. More documentation is available on the [Elasticsearch Curator wiki](https://github.com/elasticsearch/curator/wiki/Examples). You can add any of `minute`, `hour`, `day`, `weekday`, and `month` to the cron jobs—values that are not explicitly set will default to `*`.

## Dependencies

  - geerlingguy.repo-epel (RedHat/CentOS only)

## Example Playbook

    - hosts: logstash
      tasks:
      - name: Set up curator
        import_role:
          wipash.elasticsearch-curator
        vars:
          elasticsearch_curator_hosts: a918723987987.something.aws.found.io
          elasticsearch_curator_port: 9243
          elasticsearch_curator_ssl: true
          elasticsearch_curator_http_auth: username:password
          elasticsearch_curator_prefixes:
          - {
            prefix: "mylogs-",
            days_to_delete: 180,
            days_to_close: 180
          }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
