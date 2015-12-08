---
title: "Upgrading from 0.2.1"
excerpt: ""
---
[block:callout]
{
  "type": "info",
  "body": "Users who are running on OVH systems will need to update their kernel before installing Scales, documentation for that can be [found here](doc:switching-ovh-kernels). Most kernels will work fine, such as the default DigitalOcean, Linode, and Vultr kernels. If you are unsure about this step we suggest asking us on IRC or on the forums and also check out our [kernel support page](doc:check-server-kernel)."
}
[/block]
To upgrade from 0.2.1 please follow the instructions below. Please make sure that Scales is stopped before doing this.
[block:callout]
{
  "type": "danger",
  "body": "You should always backup your data before upgrading Scales, just in case. We suggest backing up the `/data` directory, your SSL Certificates, and the `config.json` file."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "cd /tmp\n\n# Upgrade Docker\nsudo apt-get upgrade docker-engine\n\n# Check Docker Version\n# Version should be 1.9.0 or higher.\ndocker version\n\n# Move into the Scales Directory\ncd /srv/scales\n\n# Fetch git changes\ngit fetch\n\n# Stash any File Changes, this might ask for some info, please perform the commands it asks for and then run it again.\ngit stash\n\n# Move to new tag\ngit checkout -f tags/0.2.3\n\n# Install the dependiencies for Scales to run.\n# This process may take a few minutes to complete.\nsudo npm update\n\n# Finish by having Scales update your images and containers.\nsudo node upgrade.js\n\n# Start Scales Again\nsudo npm start",
      "language": "shell"
    }
  ]
}
[/block]