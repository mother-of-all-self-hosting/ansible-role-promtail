# Promtail Ansible Role
**WIP role, use with caution**  
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
# promtail                                                             #
#                                                                      #
########################################################################

promtail_enabled: true

########################################################################
#                                                                      #
# /promtail                                                            #
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
### Scraping logs
#### Default scraping behavior
By default, promtail will scrape systemd-journald annd ssh logs you can enable/disable this behavior by setting :

```
promtail_journald_scraper_enabled: false
promtail_ssh_scraper_enabled: false
```
#### Scraping other logs
*Exemple with ssh:*  

Use ``promtail_container_additional_mounts_custom`` to add volumes to monitor:
```
promtail_container_additional_mounts_custom:
 - "type=bind,source=/var/log/secure,target=/data/ssh,readonly"
```


Use ``promtail_config_scrape_additional`` to define your scraping configuration:
```
promtail_config_scrape_additional: |
  - job_name: ssh
    static_configs:
    - localhost
      __path__: /data/ssh
      labels:
        job: ssh
```

## Usage

After [installing](../installing.md), ...

