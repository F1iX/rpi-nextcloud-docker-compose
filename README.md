# Nextcloud for Raspberry Pi
This repository contains a `docker-compose.yml` file to deploy a Nextcloud instance on a Raspberry Pi. Successfuly tested on a Raspberry Pi 4 B running Raspberry Pi OS Lite buster.

It uses the plain official Nextcloud (not NextCloudPi) Docker image as well as MariaDB and LetsEncrpyt through an nginx-proxy.
The images `mariadb`, `nginx-proxy` and `letsencrypt-nginx-proxy-companion` are replaced with custom builds for `armhf` architectures with special thanks to [alexanderkrause](https://github.com/Alexander-Krause/rpi-docker-letsencrypt-nginx-proxy-companion) and [jsurf](https://hub.docker.com/r/jsurf/rpi-mariadb).

## Prerequisites
- [Docker installation](https://phoenixnap.com/kb/docker-on-raspberry-pi)
- [`docker-compose` installation](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)
- Public IP (using i.e. DynDNS, MyFRITZ!, ...) and (sub-) domain pointing to it
- Port redirection for external connections on port 80 and 443

## Deployment
1. Configure variables and credentials and save files as `nextcloud-variables.env` and `mysql-variables.env`
1. Configure the volume holding your Nextcloud user data
    - Mount an external HDD, e.g. to `/media/usbssd`
    - Create a folder, e.g. `/media/usbssd/nextcloud-data`
    - `chown www-data:root /media/usbssd/nextcloud-data`
    - `chmod 770 /media/usbssd/nextcloud-data`
    - ...or delete the line `- /media/usbssd/nextcloud-data:/var/www/html/data` to simply use the main Docker volume `nextcloud` for your data
1. Run `docker-compose up -d`
1. Navigate to your domain, configure database to MySQL on host `db` with the credentials specified in `mysql-variables.env`
1. Enjoy your nextcloud instance!
