# Ansible Role: traefik

Installs traefik as a reverse proxy.

## Mandatory variables

Traefik will only listen on the address provided:

```
traefik__listen_address: "{{ ansible_host }}"
```

Traefik will read all yaml files for its dynamic configuration provided through the inventory with the variable _traefik__dynamic_config_templates_.

```
traefik__dynamic_config_templates:
- "{{ inventory_dir }}/templates/traefik/devvault01-proxy.yml"
```
