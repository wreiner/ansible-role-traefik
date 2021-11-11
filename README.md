# Ansible Role: traefik

Installs traefik as a reverse proxy.

## Mandatory variables

Traefik will only listen on the address provided:

```
traefik__listen_address: "{{ ansible_host }}"
```

This role deploys standard entrypoint of 443TCP through the variable _traefik__entrypoints_. It should be overwritten through host_vars or group_vars.

```
traefik__entrypoints:
  entryPoints:
    websecure:
      address: "{{ traefik__listen_address }}:443/tcp"
    ssh-highport:
      address: "{{ traefik__listen_address }}:2222/tcp"
```

Traefik will read all yaml files for its dynamic configuration provided through the inventory with the variable _traefik__dynamic_config_templates_.

```
traefik__dynamic_config_templates:
- "{{ inventory_dir }}/templates/traefik/devvault01-proxy.yml"
```
