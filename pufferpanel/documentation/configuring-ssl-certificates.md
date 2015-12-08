---
title: "Configuring SSL Certificates"
excerpt: ""
---
[block:callout]
{
  "type": "info",
  "body": "This tutorial is written for setting up Scales instances with SSL. However, for the most part it is pretty similar for your webserver, and tutorials can be easily found online."
}
[/block]
SSL certificates are required to run [Scales](http://scales.pufferpanel.com/) with PufferPanel, and are highly suggested for your PufferPanel instance. For your main PufferPanel website the easiest option would be to configure [CloudFlare](https://cloudflare.com) which can provide a free SSL certificate for your site.

However, you will need to either generate your own certificate or purchase one for your Scales instances. You might be wondering why we even require this, and the simple answer is that we transmit so much data between servers that we want things to be as secure as possible, and encrypting data in transport is just one way that we do this. Before you ask, no there is no (approved) way to run Scales that doesn't require using a SSL/TLS certificate.
[block:api-header]
{
  "type": "basic",
  "title": "Signing Authorities"
}
[/block]
* [Digicert](https://www.digicert.com)
* [Comodo](https://ssl.comodo.com)
* [Thawte](https://www.thawte.com/ssl/)
* [Symantec](http://www.symantec.com/ssl-certificates/)
* [Geotrust](https://www.geotrust.com/ssl/)
* [RapidSSL](https://www.rapidssl.com)
[block:api-header]
{
  "type": "basic",
  "title": "Signed Certificates"
}
[/block]
Generating a signed certificate is recommended for anyone who is running PufferPanel in a live environment. The first thing we need to do is generate a *Certificate Signing Request (CSR)* which we will provide to our signing authority.
[block:code]
{
  "codes": [
    {
      "code": "cd /srv/scales\nopenssl req -new -newkey rsa:4096 -nodes -keyout https.key -out yourdomain.csr",
      "language": "shell"
    }
  ]
}
[/block]
This should output something similar to this:
[block:code]
{
  "codes": [
    {
      "code": "-----\nYou are about to be asked to enter information that will be incorporated\ninto your certificate request.\nWhat you are about to enter is what is called a Distinguished Name or a DN.\nThere are quite a few fields but you can leave some blank\nFor some fields there will be a default value,\nIf you enter '.', the field will be left blank.\n-----\nCountry Name (2 letter code) [AU]:US\nState or Province Name (full name) [Some-State]:New York\nLocality Name (eg, city) []:New York\nOrganization Name (eg, company) [Internet Widgits Pty Ltd]:PufferPanel\nOrganizational Unit Name (eg, section) []:SSL\nCommon Name (e.g. server FQDN) []:example.yourdomain.tld\nEmail Address []:email@example.com\n\nPlease enter the following 'extra' attributes\nto be sent with your certificate request\nA challenge password []:\nAn optional company name []:",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "",
  "body": "It is critically important that you fill out this CSR with correct information. When it asks for `Common Name (e.g. server FQDN) []:` you must enter the Fully Qualified Domain Name (e.g. `scales.example.com`) or this request will fail and be an invalid certificate. Do **not** enter an IP address here, it **must** be a FQDN."
}
[/block]
After this you will need to provide this CSR to your signing authority which will guide you through some additional steps and generate your certificate for you. You can run `cat yourdomain.csr` to output the request. After this is done, download them, and you will need to then upload your certificate to the server running Scales, and then edit the `config.json` to point to these certificate files. Restart Scales and everything should be running securely.
[block:api-header]
{
  "type": "basic",
  "title": "Self-Signed Certificates"
}
[/block]
Do not use self-signed certificates on public installations where customers will have access. They display a nasty warning, and can scare customers. Additionally, if you sign them wrong it is really easy to make it impossible for PufferPanel to connect to the Scales instance. Login to your Scales server and execute the commands below to get started.
[block:code]
{
  "codes": [
    {
      "code": "cd /srv/scales\nopenssl req -x509 -days 365 -newkey rsa:4096 -keyout https.key -out https.pem -nodes",
      "language": "shell"
    }
  ]
}
[/block]
This should output something similar to below:
[block:code]
{
  "codes": [
    {
      "code": "-----\nYou are about to be asked to enter information that will be incorporated\ninto your certificate request.\nWhat you are about to enter is what is called a Distinguished Name or a DN.\nThere are quite a few fields but you can leave some blank\nFor some fields there will be a default value,\nIf you enter '.', the field will be left blank.\n-----\nCountry Name (2 letter code) [AU]:US\nState or Province Name (full name) [Some-State]:New York\nLocality Name (eg, city) []:New York\nOrganization Name (eg, company) [Internet Widgits Pty Ltd]:PufferPanel\nOrganizational Unit Name (eg, section) []:SSL\nCommon Name (e.g. server FQDN) []:example.yourdomain.tld\nEmail Address []:email@example.com\n\nPlease enter the following 'extra' attributes\nto be sent with your certificate request\nA challenge password []:\nAn optional company name []:",
      "language": "text"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "",
  "body": "It is critically important that you fill out this CSR with correct information. When it asks for `Common Name (e.g. server FQDN) []:` you must enter the Fully Qualified Domain Name (e.g. `scales.example.com`) or this request will fail and be an invalid certificate. Do **not** enter an IP address here, it **must** be a FQDN."
}
[/block]
After doing this you should be able to start Scales and your instance will be accessible over a secure connection. You will need to tell your computer to trust this certificate when viewing the webpage, and if the information above is filled out wrong PufferPanel will be unable to connect to Scales.

For Firefox you will have to make 2 exceptions, one for `scales.example.com:5656`, and `scales.example.com:5657`.
For Opera you will need to go to `scales.example.com:5656` and accept the certificate every time you start your browser.