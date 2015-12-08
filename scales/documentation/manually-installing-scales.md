---
title: "Manually Installing Scales"
excerpt: "This page will help you get started with Scales. You'll be up and running in a jiffy!"
---
[block:api-header]
{
  "type": "basic",
  "title": "Installing Dependencies"
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "Docker requires a 64-bit installation regardless of your Ubuntu version. Additionally, your kernel **must** be `3.10` at minimum. The latest `3.10` minor version or a newer maintained version are also acceptable. You can check your kernel version by running `uname -r`."
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "STOP: OVH Server Kernels",
  "body": "If you are currently running a server from OVH that is using an OVH issued kernel *you must switch kernels* before continuing to use Scales. *Scales will not work with a default OVH kernel due to cgroup issues.* Please see [this guide](http://scales.pufferpanel.com/docs/switching-ovh-kernels) for a quick kernel update."
}
[/block]
Running Scales requires the following dependencies be installed on your system. The commands below will install those dependencies for you.

`OpenSSL, cURL, git, make, gcc, g++, NodeJS, Docker, java, tar`
[block:code]
{
  "codes": [
    {
      "code": "# Install NodeJS Dependencies\ncurl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -\n\n# Install Other Dependencies\nsudo apt-get update\nsudo apt-get install -y openssl curl git make gcc g++ nodejs default-jdk tar\n\n# Install Docker\ncurl -sSL https://get.docker.com/ | sh\n\n# Add your user to the docker group\nsudo usermod -aG docker USERNAME\n\n# Check that we have succeeded.\ndocker run hello-world",
      "language": "shell",
      "name": "Ubuntu & Debian"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Docker Documentation",
  "body": "If you are having issues with any of the docker related commands above please read their documentation available [here](https://docs.docker.com/installation/ubuntulinux/#create-a-docker-group)."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Configuring SFTP"
}
[/block]
We first need to configure a few things to create user accounts that are jailed to their directory.
[block:code]
{
  "codes": [
    {
      "code": "# Add the Scales User Group\naddgroup --system scalesuser\n\n# Edit our SFTP Configuration\nsudo nano /etc/ssh/sshd_config",
      "language": "shell",
      "name": "Ubuntu"
    }
  ]
}
[/block]
First, fine the line similar to `Subsystem sftp ...` and modify it to be `Subsystem sftp internal-sftp`. After doing that scroll to the bottom and add the lines below which will configure the SFTP server correctly.
[block:code]
{
  "codes": [
    {
      "code": "Match group scalesuser\n    ChrootDirectory %h\n    X11Forwarding no\n    AllowTcpForwarding no\n    ForceCommand internal-sftp",
      "language": "text"
    }
  ]
}
[/block]
Save the file and then execute `service ssh restart`.
[block:api-header]
{
  "type": "basic",
  "title": "Installing Scales"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "# Clone the repository\ngit clone https://github.com/PufferPanel/Scales /srv/scales\n\ncd /srv/scales\n\n# Checkout the Latest Version of Scales\ngit checkout tags/$(git describe --abbrev=0 --tags)\n\n# Install the dependiencies for Scales to run.\n# This process may take a few minutes to complete.\nnpm install",
      "language": "shell"
    }
  ]
}
[/block]
We then need to create some SSL certificates to keep traffic secure between PufferPanel and Scales. You can either self-sign certificates or use signed certificates, tutorials for both can be [found here](http://www.pufferpanel.com/docs/configuring-ssl-certificates).
[block:callout]
{
  "type": "danger",
  "title": "STOP: YOU MUST GENERATE SSL CERTIFICATES.",
  "body": "Please see [this documentation](http://www.pufferpanel.com/docs/configuring-ssl-certificates) for how to complete this process."
}
[/block]
The final step is to start the server, this can be done by running the command below.
[block:callout]
{
  "type": "info",
  "body": "Make sure that you have created a node in PufferPanel before starting Scales. When you create a node in PufferPanel it will provide you with a JSON configuration. Paste that configuration into a file called `config.json` in the `/srv/scales` directory.",
  "title": "Important"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "# The command below *must* be run in the /srv/scales directory.\n# i.e. cd /srv/scales\n\n# Start Scales in the Background\nsudo npm start\n\n# Stop Scales\nsudo npm stop\n\n# Run Scales in the Foreground (verbose mode)\nsudo npm run-script start-verbose",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "success",
  "body": "You have successfully installed Scales on your system if you've reached this step. If you are having issues with Scales or PufferPanel feel free to ask for help on our [community forums](https://community.pufferpanel.com) or [in IRC](http://webchat.esper.net?channels=#pufferpanel) (irc.esper.net #pufferpanel). Please be sure to provide the logs from Scales (`/srv/scales/logs`) and from PufferPanel (`src/logs/*.log`).",
  "title": "All Done!"
}
[/block]