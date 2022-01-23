# Homelab

## The Host
OS: Debian 11
Domain: homelab.home
Account: joshua

### Data Share
mkfs.btrfs -m raid10 -d raid10 /dev/sdb /dev/sdc /dev/sdd /dev/sde
### VM volumes
mount /dev/nvme0n1 /var/lib/libvirt/images

## Docker Containers
### Jellyfin
[Jellyfin](https://hub.docker.com/r/linuxserver/jellyfin)
homelab.home:8096

### Nextcloud
[Nextcloud](https://hub.docker.com/r/linuxserver/nextcloud)
homelab.home

### Sickchill
[SickChill](https://hub.docker.com/r/linuxserver/sickchill)
homelab.home:8081

### Transmission
[Transmission](https://hub.docker.com/r/linuxserver/)
homelab.home:9091

## Virtual Machines
### Home Assistant