---
title: "Autoupdating Source Dedicated Servers"
excerpt: ""
---
Setting up your Source Server (such as Team Fortress or Insurgency) to auto-update is a simple task within PufferPanel.

The first step is to add some additional startup parameters for the server, shown below.
[block:code]
{
  "codes": [
    {
      "code": "-autoupdate -steam_dir steamcmd -steamcmd_script /home/container/steamcmd/autoupdate.txt",
      "language": "text"
    }
  ]
}
[/block]
In the `/home/container/steamcmd/autoupdate.txt` file (which you will be seeing as `/public/steamcmd/autoupdate.txt`) we need to add the following code, replacing `<APP_ID>` with the application ID for the game.
[block:code]
{
  "codes": [
    {
      "code": "login anonymous\nforce_install_dir ..\napp_update <APP_ID>\nquit",
      "language": "text",
      "name": ""
    }
  ]
}
[/block]
After this, simply restart your server and it should begin checking for updates whenever you start the server.
[block:callout]
{
  "type": "warning",
  "body": "Some games may require additional parameters in the `autoupdate.txt` file."
}
[/block]