# Phansible Role: Elasticsearch

[![CI](https://github.com/phansible/role-elasticsearch/actions/workflows/ci.yml/badge.svg)](https://github.com/phansible/role-elasticsearch/actions/workflows/ci.yml)

An Ansible Role that installs [Elasticsearch](https://www.elastic.co/products/elasticsearch) on Ubuntu and Debian specifically created with [Phansible](http://phansible.com/) in mind.

## Requirements

- Ubuntu 22.04, 24.04, 26.04 or Debian 12, 13 (x86_64)
- Ansible >= 2.15

Elasticsearch is installed from Elastic's official apt repository and runs on the JDK bundled with the package, so no system Java is needed.

## Role Variables

| Variable | Default | Description |
| --- | --- | --- |
| `elasticsearch_version` | `'9'` | Major version; selects the `<major>.x` channel of the Elastic apt repository. |
| `elasticsearch_port` | `'9200'` | HTTP port written to `http.port` in `elasticsearch.yml`. |
| `elasticsearch_heap_size` | `''` | JVM heap (for example `512m` or `2g`). Empty leaves Elasticsearch to size the heap from available memory. |
| `elasticsearch_security_enabled` | `true` | When `false`, turns off security, enrollment and TLS so the node serves plain HTTP without authentication. Only for local development. |

With `elasticsearch_security_enabled: true` the package's defaults apply: security is enabled on first install (TLS on HTTP and a generated `elastic` password). Reset the password with `/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic`.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: search
  become: yes
  vars:
    elasticsearch_heap_size: 1g
  roles:
    - role-elasticsearch
```

## License

This role is released under the terms of the license specified in the repository or if not specified, under the [MIT license](https://raw.githubusercontent.com/phansible/role-elasticsearch/master/LICENSE).

## Author Information

This role was created in 2015 by [The Phansible Team & Contributors](https://github.com/phansible/role-elasticsearch/graphs/contributors), credits go also to [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/) and source of inspiration.
