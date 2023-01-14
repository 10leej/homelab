# Homelab

## System 1: Lab
OS: Fedora 37
Hostname: lab.10leej.com

### Data Share
mkfs.btrfs -m raid10 -d raid10 /dev/sdb /dev/sdc /dev/sdd /dev/sde

### Docker Containers
#### nginx
[NGINX](https://hub.docker.com/r/linuxserver/nginx)
192.168.0.2

#### Sickchill
[SickChill](https://hub.docker.com/r/linuxserver/sickchill)
192.168.0.2:8081

#### Transmission
[Transmission](https://hub.docker.com/r/linuxserver/)
192.168.0.2:9091

#### Jellyfin
192.168.0.2: 8096

#### UpTime Kuma
192.168.0.2: 3001

#### NextCloud

#### MariaDB

### Virtual Machines
#### HomeAssistant OS


## System 2: Backup
