# Promtail Ansible Role

[promtail](https://grafana.com/oss/promtail/) is a log aggregation system designed to store and query logs from all your applications and infrastructure. This role helps you to set up promtail:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official promtail container image](https://hub.docker.com/r/grafana/promtail/)


## Installing

To configure and install promtail on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

## Configuration

To enable this service, add the following configuration to your `vars.yml` file and re-run the [installation](../installing.md) process:

```yaml
########################################################################
#                                                                      #
# promtail                                                                 #
#                                                                      #
########################################################################

promtail_enabled: true

########################################################################
#                                                                      #
# /promtail                                                                #
#                                                                      #
########################################################################
```

### Exposing the web interface

By setting a hostname you will expose promtail on this domain.
Usually you should also set up basic_auth in this case, otherwise everyone will be able to access your metrics

```yaml
promtail_hostname: promtail.example.org

# Uncommenting the following lines allows you to configure basic auth
# promtail_basic_auth_enabled: true
# promtail_basic_auth_username: ''
# promtail_basic_auth_password: ''
```

## Usage

After [installing](../installing.md), refer to the [official documentation](https://grafana.com/docs/promtail/latest/reference/api/#post-promtailapiv1push) to send logs throught promtail's API without an agent.
The [Promtail agent](https://grafana.com/docs/promtail/latest/send-data/promtail/) is coming soon
