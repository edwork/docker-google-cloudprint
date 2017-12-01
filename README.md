![logo](logo.png "Raspberry PI - Google Cloudprint - Docker Image")

Raspberry PI - Google Cloudprint - Docker Image
===============================================

[![latest release](https://img.shields.io/github/release/jaymoulin/docker-rpi-google-cloudprint.svg "latest release")](http://github.com/jaymoulin/docker-rpi-google-cloudprint/releases)
[![Docker Pulls](https://img.shields.io/docker/pulls/jaymoulin/rpi-google-cloudprint.svg)](https://hub.docker.com/r/jaymoulin/rpi-google-cloudprint/)
[![Docker Stars](https://img.shields.io/docker/stars/jaymoulin/rpi-google-cloudprint.svg)](https://hub.docker.com/r/jaymoulin/rpi-google-cloudprint/)
[![Bitcoin donation](https://github.com/jaymoulin/jaymoulin.github.io/raw/master/btc.png "Bitcoin donation")](https://m.freewallet.org/id/374ad82e/btc)
[![Litecoin donation](https://github.com/jaymoulin/jaymoulin.github.io/raw/master/ltc.png "Litecoin donation")](https://m.freewallet.org/id/374ad82e/ltc)
[![PayPal donation](https://github.com/jaymoulin/jaymoulin.github.io/raw/master/ppl.png "PayPal donation")](https://www.paypal.me/jaymoulin)

This image allows you to configure your printer to your Google Cloudprint easily thanks to Docker.

Installation
---

```
docker run -d --privileged --restart=always -v /dev/bus/usb:/dev/bus/usb --name cloudprint -e CUPS_USER_ADMIN=admin -e CUPS_USER_PASSWORD=password -p 631:631 jaymoulin/rpi-google-cloudprint
```

You can change your admin login/password by replacing values for `CUPS_USER_ADMIN` and `CUPS_USER_PASSWORD`.

Configuration
---
First, allow administration interface to be accessed to setup your printer:
```
docker exec cloudprint configure open
```
This will allow your printer to be configured. 
Go to http://__raspberry_ip__:631 to configure it

Login/Password couple defined with `$CUPS_USER_ADMIN` `$CUPS_USER_PASSWORD` in installation command

Once configured, close admin interface to secure it up and retrieve your Google Cloudprint URL.

```
docker exec -t cloudprint configure close
```

It will give you a Google Link. Copy/paste this URL in your browser to claim your printer, and voila!

Updating
-----

When Google Cloudprint new version is released, you will be able to update your running version with this command:
 
```
docker exec -t cloudprint configure update
```

Appendixes
---

### Install RaspberryPi Docker

If you don't have Docker installed yet, you can do it easily in one line using this command
 
```
curl -sSL "https://gist.githubusercontent.com/jaymoulin/e749a189511cd965f45919f2f99e45f3/raw/0e650b38fde684c4ac534b254099d6d5543375f1/ARM%2520(Raspberry%2520PI)%2520Docker%2520Install" | sudo sh && sudo usermod -aG docker $USER
```

### Build Docker Image

To build this image locally 
```
docker build -t jaymoulin/rpi-google-cloudprint .
```
