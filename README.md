# Ansible Role: Elasticsearch Curator

[![Build Status](https://travis-ci.org/mtnsat/ansible-role-elasticsearch-curator.svg?branch=master)](https://travis-ci.org/mtnsat/ansible-role-elasticsearch-curator)

An Ansible Role that installs [Elasticsearch Curator](https://github.com/elasticsearch/curator) on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None, but it's a lot more helpful if you have Elasticsearch running somewhere :)

On RedHat/CentOS, make sure you have the EPEL repository configured, so the `python-pip` package can be installed. You can install the EPEL repo by simply adding `geerlingguy.repo-epel` to your playbook's roles.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticsearch_curator_version: 4.2.5
    elasticsearch_curator_hosts:
      - 127.0.0.1
    elasticsearch_curator_port: 9200
    elasticsearch_curator_master_only: False

    elasticsearch_curator_cron_jobs:
      - {
        name: "elasticsearch_curator",
        job: "/usr/local/bin/curator /etc/curator/curator.yml",
        minute: 5,
        hour: 0
      }


A list of cron jobs to use curator to prune, optimize, close, and otherwise maintain your Elasticsearch indexes. More documentation is available on the [Elasticsearch Curator wiki](https://github.com/elasticsearch/curator/wiki/Examples). You can add any of `minute`, `hour`, `day`, `weekday`, and `month` to the cron jobs—values that are not explicitly set will default to `*`.

## Dependencies

  - geerlingguy.repo-epel (RedHat/CentOS only)

## Example Playbook

    - hosts: search
      roles:
        - { role: mtnsat.elasticsearch-curator }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
