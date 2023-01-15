# Homelab
This is my notes and plans for my home infurastructure. I'm gonna keep as much of the publicly "safe to post" data here as I can.

This repo is primarily hosted at [GitLab](https://gitlab.com/10leej/homelab) but a mirror is on [GitHub](https://github.com/10leej/homelab) since it's a popular website.

## System 1: Lab
OS: Fedora 37
Hostname: lab.10leej.com

### Data Mounts

Our filesystem of choice is btrfs, two arrays, first array is raid 10 second array is raid 0 for the game library

#### Primary Data Drive
First lets generate the raid 10 array which will hold the majority of our files, I use 6TB Seagate Ironwolf Pro drives which IMO are plenty enough for me. Lighted at this time the cost of Terabyte per Dollar says the larger disks are better, but these are what i deem "wallet affordable" as to me 1 disk is physically 2 disks.
Raid10 should give us a nice blend of read/write performance and still single disk redundancy. There's a chance I might test a raid 5/6 array in the future, but those are still experimental in btrfs

`` mkfs.btrfs -m raid10 -d raid10 -L DATA /dev/sdb /dev/sdc /dev/sdd /dev/sde ``

After making the file system we created five subvolumes

`` btrfs subvolume create backups ``
`` btrfs subvolume create containers ``
`` btrfs subvolume create games ``
`` btrfs subvolume create media ``
`` btrfs subvolume create sync ``

We then go back and mount these all in the appropriate folder in /mnt appending this into out fstab

````
LABEL=DATA /mnt/backups btrfs compress=zstd,datacow,subvol=backups 0 0
LABEL=DATA /mnt/containers btrfs compress=zstd,datacow,subvol=containers 0 0
LABEL=DATA /mnt/games btrfs compress=zstd,datacow,subvol=games 0 0
LABEL=DATA /mnt/media btrfs compress=zstd,datacow,subvol=media 0 0
LABEL=DATA /mnt/sync btrfs compress=zstd,datacow,subvol=sync 0 0
````

#### Game Drive
Now we generate the game drive using our two 500GB crucial SATA ssd's

`` mkfs.btrfs -m raid0 -d raid0 -L GAME /dev/sda /dev/sdf ``

Then we setup the appropriate subvolume
`` btrfs subvolume create games ``

I'm aware that subvolume name matches the same one above, and they we have two game subvolumes which makes no sense upfront. There's logic here. I have a slow internet connection and downloading large games just don't work when my ISPs steam cache doesn't already have a game cache'd. So I keep my entire steam library in the big data share.
This faster array is for games that like faster read times.

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
[Official Docs](https://jellyfin.org/docs/general/installation/container/)
192.168.0.2:8096

#### UpTime Kuma
[UpTime Kuma](https://uptime.kuma.pet/)
192.168.0.2:3001

#### NextCloud
[NextCloud on Fedora Magazine](https://fedoramagazine.org/nextcloud-20-on-fedora-linux-with-podman/)
192.168.0.2:8080

Had to open port 8080/tcp since we want to run the container rootless.

#### MariaDB
[NextCloud on Fedora Magazine](https://fedoramagazine.org/nextcloud-20-on-fedora-linux-with-podman/)

This was setup in the same subnet as nextcloud, we might expand it in the future.

### Virtual Machines

I manage my VM's mostly through virt-manager, but we'lkl experiment with cockpit

#### HomeAssistant OS
[Website](https://www.home-assistant.io/)
We'll try the [KVM image](https://www.home-assistant.io/installation/linux)

## System 2: Backup
OS: Fedora 37

This has yet to be fully confuigured but for now it does hold rsync snapshots from System 1, though the backups are not automated.

## System 3: Webserver
OS: Debian 11 (Grandfathered)

## System 4: Private VPS
OS: Fedora 37
