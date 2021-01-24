# Anki-Sync-Server for Raspberry Pi with https
This repository contains a `docker-compose.yml` file to deploy a Anki-Sync-Server instance on a Raspberry Pi with a reverse-proxy to enable TLS (https) for communication with the AnkiDroid App.
AnkiDroid does not accept non-https servers as of version 2.11.

It uses the Docker image from ankicommunity/docker-anki-sync-server as well as LetsEncrpyt through an nginx-proxy.
Special thanks to [kuklinistvan](https://github.com/kuklinistvan) for his work on the docker-anki-sync-server repository mentioned above.
The images `nginx-proxy` and `letsencrypt-nginx-proxy-companion` are builds for `armhf` architectures thanks to [alexanderkrause](https://github.com/Alexander-Krause/rpi-docker-letsencrypt-nginx-proxy-companion).

## Prerequisites
- [Docker installation](https://phoenixnap.com/kb/docker-on-raspberry-pi)
- [`docker-compose` installation](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)
- Public IP (using i.e. DynDNS, MyFRITZ!, ...) and (sub-) domain pointing to it
- Port redirection for external connections on port 80 and 443

## Deployment
1. Clone this repository including the submodules with `git clone --recurse-submodules https://github.com/ankicommunity/docker-anki-sync-server.git`
2. Configure variables and credentials in `anki-variables.env`
3. Create the folder holding your anki user data and enter it in the docker-compose.yml file 
Example: `- /media/usbssd/anki-data:/app/data`
4. Run `docker-compose up -d --build` from within the directory containing the docker-compose.yml
5. Add/Configure users by sending the appropriate commands to the administration interface inside container `anki-server` with
`docker exec anki-server /app/anki-sync-server/ankisyncctl.py YOURCOMMANDHERE`
`
    Commands:
      adduser <username> - add a new user
      deluser <username> - delete a user
      lsuser             - list users
      passwd <username>  - change password of a user
`
