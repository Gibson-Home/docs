---
title: Pi-hole
layout: page
parent: Containers
---

# Pi-hole

Pi-hole is providing DNS with Filtering and DHCP.

Some devices have reservations created in DHCP to provide static ip addresses.

Custom cname records are created for internal services.

## Docker Compose

Update _REPLACE_ME_ with an administrator password.


```
---
version: '3'
services:
  pihole:
    container_name: pihole
    image: docker.io/pihole/pihole:latest
    restart: unless-stopped
    # For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
    network_mode: host
    environment:
      PIHOLE_UID: 1000
      PIHOLE_GID: 1000
      INTERFACE: ens192
      TZ: America/New_York
      WEBPASSWORD: REPLACE_ME
      WEBTHEME: default-dark
      TEMPERATUREUNIT: f
      FTLCONF_LOCAL_IPV4: 172.18.69.254
    volumes:
      - pihole-etc-pihole:/etc/pihole
      - pihole-etc-dnsmasq.d:/etc/dnsmasq.d
      # - ./pihole/etc-pihole:/etc/pihole
      # - ./pihole/etc-dnsmasq.d:/etc/dnsmasq.d
    # https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN  # Required if you are using Pi-hole as your DHCP server, else not needed
      - NET_RAW

volumes:
  pihole-etc-pihole:
  pihole-etc-dnsmasq.d:
```

## Resources

[https://pi-hole.net/](https://pi-hole.net/)
