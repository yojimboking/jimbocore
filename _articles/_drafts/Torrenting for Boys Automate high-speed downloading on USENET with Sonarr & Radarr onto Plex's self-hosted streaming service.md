---
published: false
subtitle:
date: 08-01-22
tags: neet lifestyle
---



# Torrenting for Boys: Automate high-speed downloading on USENET with Sonarr & Radarr onto Plex's self-hosted streaming service


## Software Stack

![[Pasted image 20220906020844.png]]

**Downloaders**:

-   [Deluge](http://deluge-torrent.org/): torrent downloader with a web UI
-   [NZBGet](https://nzbget.net/): usenet downloader with a web UI
-   [Jackett](https://github.com/Jackett/Jackett): API to search torrents from multiple indexers
-   [Bazarr](https://www.bazarr.media/): A companion tool for Radarr and Sonarr which will automatically pull subtitles for all of your TV and movie downloads.

**Download orchestration**:

-   [Sonarr](https://sonarr.tv/): manage TV show, automatic downloads, sort & rename
-   [Radarr](https://radarr.video/): basically the same as Sonarr, but for movies

**VPN**:

-   [OpenVPN](https://openvpn.net/) client configured with a [privateinternetaccess.com](https://www.privateinternetaccess.com/) access

**Media Center**:

-   [Plex](https://plex.tv/): media center server with streaming transcoding features, useful plugins and a beautiful UI. Clients available for a lot of systems (Linux/OSX/Windows, Web, Android, Chromecast, Android TV, etc.)


## Hardware Stack

I'm using an old [Proliant MicroServer N54L](http://www.minimachines.net/promos-et-sorties/bon-plan-un-micro-serveur-hp-proliant-4-emplacements-a-169e-371) (2 cores, 2.20GHz) that I tweaked a bit to have 6GB RAM, an additional graphic card for better Full HD decoding, and an additional 2TB disk for data.

It has Ubuntu 17.10.1 with Docker installed.

You can also use a Raspberry Pi, a Synology NAS, a Windows or Mac computer. The stack should work fine on all these systems, but you'll have to adapt the Docker stack below to your OS. I'll only focus on a standard Linux installation here.

https://github.com/sebgl/htpc-download-box

Upgrades:
- Docker
- https://organizr.app/
- Bazaar
- Ombi
- RAID setup


![[Pasted image 20220906020719.png]]

---

# Installation Guide

The stack is not plug-and-play, manual configuration is required as well as setting some external accounts (usenet indexers, torrent indexers, vpn server, plex account, etc.) but everything will be persisted on reboots. All components will be setup in Docker containers in a docker-compose.yml file using community-maintained images. 

## Setup Docker

### Install docker and docker-compose

Download [Docker desktop](https://www.docker.com/products/docker-desktop/) and follow the steps to install it on your machine.

Once the installation is complete, open the application.

Accept the subscription:

### Clone Repo and Run Setup
Clone the git repo located at [sebgl/htpc-download-box](https://github.com/sebgl/htpc-download-box)

This is where you will run the full setup from (note: this isn't the same as your media directory). 


### Setup environment variables
Navigate to the folder where you saved the repo, and you'll see a file called `.env.example`. Rename it to `.env`.

Next we'll edit the `.env` file to your local settings:

```
# Your timezone, https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
TZ=America/New_York
PUID=1000
PGID=1000
# The directory where data and configuration will be stored.
ROOT=/media/my_user/storage/homemedia
```

Things to notice:

-   TZ is based on your [tz time zone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
-   The PUID and PGID are your user's ids. Find them with `id $USER`.
-   This file should be in the same directory as your `docker-compose.yml` file so the values can be read in.

### Compose Docker

Open Terminal (cmd on Windows) and navigate to where you saved the repo:
`cd path/to/repo`

Then run:
`docker compose up`

Wait for the automated setup to complete. 

Once it's done, you'll see the applications installed in Docker Desktop, under Containers.

## Setup Deluge

Deluge's web UI is located on port `8112`. Goto your browser and enter `localhost:8112` in the url.

![[Pasted image 20220916004517.png]]

The default password is `deluge`. You are asked to modify it, I chose to set an empty one since deluge won't be accessible from outside my local network.

The running deluge daemon should be automatically detected and appear as online. Hit `connect`
![[Pasted image 20220916004552.png]]

You may want to change the download directory. I like to have to distinct directories for incomplete (ongoing) downloads, and complete (finished) ones.

![[Pasted image 20220916004713.png]]

You can also use the Web UI manually to download any torrent from a .torrent file or magnet hash.

## Setup a VPN Container

The goal here is to have an OpenVPN Client container running and always connected. We'll make Deluge incoming and outgoing traffic go through this OpenVPN container.

This must come up with some safety features:

1.  VPN connection should be restarted if not responsive
2.  Traffic should be allowed through the VPN tunnel _only_, no leaky outgoing connection if the VPN is down
3.  Deluge Web UI should still be reachable from the local network

---

## Setup Jackett
[Jackett](https://github.com/Jackett/Jackett) translates request from Sonarr and Radarr to searches for torrents on popular torrent websites, even though those website do not have a standard common APIs.

Jackett web UI is available on port 9117. Goto `localhost:9117` on your web browser.

[![Jacket empty providers list](https://github.com/sebgl/htpc-download-box/raw/master/img/jackett_empty.png)](https://github.com/sebgl/htpc-download-box/blob/master/img/jackett_empty.png)

Click on `Add Indexer` and add any torrent indexer that you like. I added 1337x, cpasbien, RARBG, The Pirate Bay and YGGTorrent (need a user/password).

You can now perform a manual search across multiple torrent indexers in a clean interface with no trillion ads pop-up everywhere. Then choose to save the .torrent file to the configured blackhole directory, ready to be picked up by Deluge automatically !

![[Pasted image 20220916005438.png]]