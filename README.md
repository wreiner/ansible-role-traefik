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

Traefik will read all yaml files for its dynamic configuration provided through the inventory or the playbook with the variable _traefik__dynamic_config_templates_.

For inventory and non AWX users:

```
# example inventory structure
dev
├── group_vars
│   └── all.yml
├── hosts.yml
├── host_vars
│   └── targethost.yml
└── templates
    └── traefik
        └── devvault01-proxy.yml

# host_vars/targethost.yml in inventory
traefik__dynamic_config_templates:
- "{{ inventory_dir }}/templates/traefik/devvault01-proxy.yml"
```

For AWX users the inventory is handled differently. Therefore the templates need to be placed inside the playbook:

```
# example play structure
dev-ansible-play-traefik/
├── playbook.yml
├── roles
│   └── requirements.yml
└── templates
    └── traefik
        └── devvault01-proxy.yml

# host_vars/targethost.yml in inventory
traefik__dynamic_config_templates:
- "traefik/devvault01-proxy.yml"
```