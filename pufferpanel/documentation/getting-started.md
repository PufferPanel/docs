---
title: "Getting Started with PufferPanel"
excerpt: "This page will help you get started with PufferPanel. You'll be up and running in a jiffy!"
---
The following is a list of dependencies required for PufferPanel (0.8.3) to be installed on your server. This installation guide is compatible with Ubuntu 14.04.
[block:callout]
{
  "type": "info",
  "body": "PufferPanel has been tested and works with the following operating systems: `Ubuntu 14.04 and 15.10`, `CentOS 7.1`, `Debian 8.1`. We do not support Windows based operating systems as the daemon will not run on them."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "nginx\nOpenSSL\ncURL\nPHP – 5.5 or higher\n\t- extensions required: curl, hash, openssl, mcrypt, pdo, pdo_mysql\nPHP-CLI\nMySQL – min. 5.5, suggested 5.6",
      "language": "text"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "# If you currently have Apache2 installed you will not be able to use nginx as well. Please plan accordingly.\nsudo apt-get update\nsudo apt-get install -y openssl curl nginx git mysql-client mysql-server php5-fpm php5-cli php5-curl php5-mysql php5-mcrypt\n\n# Please restart php5-fpm after running the command below\n# See http://askubuntu.com/a/460862\nphp5enmod mcrypt\nservice php5-fpm restart",
      "language": "shell",
      "name": "Ubuntu 14.04, 15.10; Debian 8.1"
    },
    {
      "code": "Due to many variations within CentOS for installing PHP 5.5+, \nwe do not have acceptable documentation for installing it. \nPlease consult guides on how to install PHP 5.5 and \nnginx for your specific CentOS version.\n\nhttps://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-centos-7",
      "language": "text",
      "name": "CentOS"
    }
  ]
}
[/block]
PufferPanel comes with an automatic installer which will guide you through the install process, and get everything set up and working for you. This installer can be downloaded [here](https://raw.githubusercontent.com/PufferPanel/Tools/master/installer/installer) or by running the command below. The installer will guide you through the entire process.
[block:code]
{
  "codes": [
    {
      "code": "curl -o /tmp/pp-install -L http://git.io/vf3F8 && sudo bash /tmp/pp-install",
      "language": "shell",
      "name": "Stable"
    }
  ]
}
[/block]
After completing the installer process, we need to modify the web server configuration files so that they will allow access to the panel . 

**To configure *nginx*, please follow this documentation**:
http://www.pufferpanel.com/docs/nginx-configuration

[block:callout]
{
  "type": "danger",
  "title": "Stop – Read This Carefully",
  "body": "Please ensure that your web-server is properly configured to prevent access to any directory within PufferPanel *except* for the `/public` directory. All others should *not be web accessible*. Failing to ensure that this step is completed could lead to unintended consequences."
}
[/block]

[block:callout]
{
  "type": "success",
  "title": "Create a Node",
  "body": "Now that PufferPanel is installed it is time to create a new node in the panel and [install Scales](http://scales.pufferpanel.com/docs/getting-started) to your node."
}
[/block]