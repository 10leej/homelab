# Homelab
This is my notes and plans for my home infurastructure. I'm gonna keep as much of the publicly "safe to post" data here as I can.

This repo is primarily hosted at [gitlab](https://gitlab.com/10leej/homelab) but a mirror is on [github](https://github.com/10leej/homelab) since it's a popular website.

## System 1: Lab
OS: Fedora 37
Hostname: lab.10leej.com

### Data Share
mkfs.btrfs -m raid10 -d raid10 /dev/sdb /dev/sdc /dev/sdd /dev/sde

### Docker Containers
Container Daemon Tool: Podman, each container will be operating under a use level service.

#### nginx
[NGINX](https://hub.docker.com/r/linuxserver/nginx)
192.168.0.2

There's a chance we might just roll this bare metal in all honesty.

#### Transmission
[Transmission](https://hub.docker.com/r/linuxserver/)
192.168.0.2:9091

I honestly and truely only use this for seeding Linux Distro's, if I'm gonna torrent anything questionable I'd use a virtual machine connected through a VPN.

#### Jellyfin
192.168.0.2:8096

#### UpTime Kuma
192.168.0.2:3001

#### NextCloud

#### MariaDB

### Virtual Machines
#### HomeAssistant OS


## System 2: Backup

## System 3: Webserver

## System 4: Private VPS
