https://countdown.eleanor.services


# Countdown


Countdown is a website that shows days, hours, minutes, and seconds remaining until the end of 2020.

## Demo
This is how this app looks :
<img src="https://raw.githubusercontent.com/kevinadhiguna/countdown/master/demo/1.png" width="90%"></img>

[![Visits Badge](https://badges.pufler.dev/visits/kevinadhiguna/countdown)](https://github.com/kevinadhiguna)


Example docker-compose v3.7 with traefik 

```
countdown:
    image: ghcr.io/mavi0/countdown:latest
    container_name: countdown
    networks:
      - traefik-network
      - default
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    restart: unless-stopped
    labels:
      - traefik.enable=true
      - traefik.http.routers.countdown.entrypoints=web
      - traefik.http.routers.countdown-sec.entrypoints=websecure
      - traefik.http.routers.countdown.rule=Host(`countdown.${DOMAIN}`)
      - traefik.http.routers.countdown-sec.rule=Host(`countdown.${DOMAIN}`)
      - traefik.http.services.countdown-sec.loadbalancer.server.port=80
      - traefik.http.routers.countdown.middlewares=basic-http
      - traefik.http.routers.countdown-sec.middlewares=basic
      - traefik.http.routers.countdown-sec.tls=true
      - traefik.http.routers.countdown-sec.tls.certresolver=cfdns
```
