---
title: cloudflared
layout: page
parent: Containers
---

# cloudflared

cloudflared provides a tunnel to publicly access internal resources without the need for port forwarding.

## Docker Compose

```
---
version: '3'

services:
  cloudflared:
    container_name: cloudflared
    image: docker.io/cloudflare/cloudflared:latest
    restart: unless-stopped
    privileged: true
    network_mode: host
    command: >
      tunnel
      --no-autoupdate run
      --token REPLACE_ME
    cap_add:
      - NET_ADMIN
      - NET_RAW
```

## Resources

[https://github.com/cloudflare/cloudflared](https://github.com/cloudflare/cloudflared)
