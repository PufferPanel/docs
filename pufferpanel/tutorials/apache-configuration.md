---
title: "Apache Configuration"
excerpt: "Configuration an Apache server for Pufferpanel support"
---
[block:callout]
{
  "type": "danger",
  "title": "CAUTION",
  "body": "This documentation is incomplete and may not be completely accurate. Please consult the Apache documentation for any problems using this."
}
[/block]
This documentation assumes you have Apache/Httpd installed. If you do not, please consult apache's documentation or the many tutorials on installing a LAMP server.

First, you must locate your root configuration for Apache/Httpd (generally */etc/httpd/httpd.config* or */etc/apache2/apache2.conf*). In that file, change/append the following.
[block:code]
{
  "codes": [
    {
      "code": "DocumentRoot /srv/PufferPanel/public\n<Directory \"/srv/PufferPanel/public\">\n    AllowOverride All\n    Order Allow,Deny\n    Allow from all\n    Require all granted\n</Directory>",
      "language": "text"
    }
  ]
}
[/block]
You can also create a virtualhost with this in it in if you host multiple websites.
[block:callout]
{
  "type": "info",
  "body": "If you are receiving \"500 Bad Request\" error, make sure to enable mod rewrite!\nType `sudo a2enmod rewrite` in your terminal following it with `sudo service apache2 restart`"
}
[/block]