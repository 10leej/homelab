# Homelab

## The Host
OS: Debian 11
Domain: home

### Data Share
mkfs.btrfs -m raid10 -d raid10 /dev/sdb /dev/sdc /dev/sdd /dev/sde

## Docker Containers
### nginx
[NGINX](https://hub.docker.com/r/linuxserver/nginx)
192.168.0.106

### Sickchill
[SickChill](https://hub.docker.com/r/linuxserver/sickchill)
homelab.home:8081

### Transmission
[Transmission](https://hub.docker.com/r/linuxserver/)
homelab.home:9091

## Virtual Machines
### Home Assistant
