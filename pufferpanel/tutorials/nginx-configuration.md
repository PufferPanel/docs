---
title: "Nginx Configuration"
excerpt: "Configuring an Nginx server for Pufferpanel support"
---
This documentation will assume you have Nginx installed. If you do not, please consult [nginx's documentation](http://wiki.nginx.org/Install) on how to install.

You will need to locate where your nginx server configs are (generally */etc/nginx*). In there, will be either a *conf.d* or a *sites-enabled* folder. In that folder, create a *pufferpanel.conf* file and add the following (replacing panel.examplehost.com with the IP address or domain to access the panel on).
[block:callout]
{
  "type": "info",
  "body": "This configuration assumes that you have PHP listening using a unix socket. Most configurations will default to using a socket, although some configure it with a TCP connection. To determine if this is the case run the command below.\n\nCentOS: `grep '^listen *=' /etc/php-fpm.d/www.conf`\nUbuntu: `grep '^listen *=' /etc/php5/fpm/pool.d/www.conf`\n\n Should this be `127.0.0.1:9000`, you may replace the `fastcgi_pass` below with `127.0.0.1:9000;`"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "server {\n    listen 80;\n    root /srv/PufferPanel/;\n    index index.php;\n    \n    server_name panel.examplehost.com;\n\n    client_max_body_size 20m;\n    client_body_timeout 120s;\n\n    location / {\n        try_files /public/router.php =404;\n        fastcgi_split_path_info ^(.+?\\.php)(/.*)$;\n        fastcgi_pass unix:/var/run/php5-fpm.sock;\n        fastcgi_index router.php;\n        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n        include /etc/nginx/fastcgi_params;\n    }\n\n    location /assets {\n        try_files /app/$uri =404;\n    }\n\n}\n\n#server {\n#    listen 443;\n#    root /srv/PufferPanel/;\n#    index index.php;\n#\n#    server_name panel.examplehost.com;\n#\n#    ssl on;\n#    ssl_certificate     /etc/nginx/ssl/<server>.crt;\n#    ssl_certificate_key /etc/nginx/ssl/<server>.key;\n#\n#    location / {\n#        try_files /public/router.php =404;\n#        fastcgi_split_path_info ^(.+?\\.php)(/.*)$;\n#        fastcgi_pass unix:/var/run/php5-fpm.sock;\n#        fastcgi_index router.php;\n#        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n#        include /etc/nginx/fastcgi_params;\n#    }\n#\n#    location /assets {\n#        try_files /app/$uri =404;\n#    }\n\n",
      "language": "shell",
      "name": "pufferpanel.conf"
    }
  ]
}
[/block]

Afterwards, use `service nginx restart` to restart nginx and apply this change.
[block:callout]
{
  "type": "info",
  "body": "This file does not permit HTTPS access to your panel directly. If you wish to use HTTPS, uncomment the second server block and point the ssl_certificate and ssl_certificate_key to those for your server. If you use Cloudflare for HTTPS support, this should not be uncommented."
}
[/block]