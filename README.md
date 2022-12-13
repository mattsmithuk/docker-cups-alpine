# cups-alpine

[![build][badge-gh-actions-build]][link-gh-actions-build]

Fork from [chuckcharlie/docker-cups-airprint](https://github.com/chuckcharlie/cups-avahi-airprint)

## Configuration

### Volumes

* `/config`: where the persistent printer configs will be stored
* `/services`: where the Avahi service files will be generated

### Variables

* `CUPSADMIN`: the CUPS admin user you want created - default is CUPSADMIN if unspecified
* `CUPSPASSWORD`: the password for the CUPS admin user - default is admin username if unspecified

### Ports/Network

* Must be run on host network. This is required to support multicasting which is needed for Airprint.

### Example run command

```sh
docker run --name cups --restart unless-stopped  --net host\
  -v <your services dir>:/services \
  -v <your config dir>:/config \
  -e CUPSADMIN="<username>" \
  -e CUPSPASSWORD="<password>" \
  chuckcharlie/cups-avahi-airprint:latest
```

## Add and set up printer

* CUPS will be configurable at http://[host ip]:631 using the CUPSADMIN/CUPSPASSWORD.
* Make sure you select `Share This Printer` when configuring the printer in CUPS.
* ***After configuring your printer, you need to close the web browser for at least 60 seconds. CUPS will not write the config files until it detects the connection is closed for as long as a minute.***

[badge-gh-actions-build]: https://github.com/g3rhard/docker-cups-alpine/actions/workflows/build.yml/badge.svg?branch=production
[link-gh-actions-build]: https://github.com/g3rhard/docker-cups-alpine/actions?query=workflow%3Abuild
