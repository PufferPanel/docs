# Prerequisites

The following guide will help you setup LetsEncrypt for Scales. We expect you to already have PufferPanel and Scales setup properly with node's added. If not, please go do so here: [PufferPanel - Getting started](https://pufferpanel.readme.io/docs/getting-started "PufferPanel - Getting started")

Note: You need one LetsEncrypt certificate per Node you have.

### Generating LetsEncrypt certificate

Make sure to follow the LetsEncrypt's generation screen.
```sh
git clone https://github.com/letsencrypt/letsencrypt && cd letsencrypt
./letsencrypt-auto certonly -d yourdomain.com
```
### Setting up Scales

```sh
cd /srv/scales
sudo npm stop #stops the Scales service
nano config.json
```
Find and change the "key" and "cert" lines to the following:

```sh
"key": "/etc/letsencrypt/live/yourdomain.com/privkey.pem",
"cert": "/etc/letsencrypt/live/yourdomain.com/cert.pem"
```
Start the scales service:
```sh
sudo npm start
```
### Last step

Make sure the Node FQDN is set to yourdomain.com as well! If its set to an IP, it will NOT work.


