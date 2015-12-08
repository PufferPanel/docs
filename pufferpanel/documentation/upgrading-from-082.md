---
title: "Upgrading from 0.8.2"
excerpt: ""
---
[block:callout]
{
  "type": "danger",
  "body": "Always make a backup of your database and files before upgrading, it is good practice and we cannot be held responsible for data loss!"
}
[/block]
Upgrading from PufferPanel 0.8.2 is a very simple process and should take less than 5 minutes. Simply run the commands below and then [update your Scales instances](http://scales.pufferpanel.com/docs/upgrading-from-021).
[block:code]
{
  "codes": [
    {
      "code": "cd /tmp\n\n# Download 0.8.3 Upgrader\ncurl -o upgrade.sh https://raw.githubusercontent.com/PufferPanel/Tools/master/upgrader/0.8.3/upgrader.sh\n\n# Update File Permissions\nchmod +x upgrade.sh\n\n# Run Script — Follow Script Prompts\n./upgrade.sh",
      "language": "shell"
    }
  ]
}
[/block]