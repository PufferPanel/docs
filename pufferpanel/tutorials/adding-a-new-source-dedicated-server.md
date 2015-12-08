---
title: "Adding a new Source Dedicated Server"
excerpt: "The Source Dedicated Server or SRCDS is a tool that runs the server component of a Source game without the client component. In other words, it simulates the game without drawing it. SRCDS is chiefly used by server providers who want to serve up as many games from the same computer as they can."
---
[block:callout]
{
  "type": "info",
  "body": "This tutorial assumes that you have PufferPanel fully installed as well as a server running a Scales instance with all required SRCDS dependencies installed."
}
[/block]
PufferPanel now supporting running SRCDS servers from the panel. This tutorial will show you how to set up a server through PufferPanel.

Begin by creating a new server and filling out the normal information at the top such as server name and owner. Allocate the server to whatever node you wish. The next step is to select `SRCDS` as the `Server Plugin`.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/4BNWTaLRqSJAVpB6CPSw",
        "Screen Shot 2015-04-24 at 9.59.33 PM.png",
        "1452",
        "360",
        "#5a8fc8",
        ""
      ],
      "caption": "Select SRCDS as the Server Plugin for this server."
    }
  ]
}
[/block]
The next step is to allocate memory and disk space to the server. Since this is a SRCDS server there is no current way to limit memory usage, so go ahead and set this to something like `1024`, and Scales does not currently handle disk space management, so you can set to  `0` if you like. SRCDS servers do consume quite a bit of CPU power depending on the game, so it may be worthwhile to put in a CPU limit. However, for the sake of this tutorial, we are going to set it to `0` since we don't want our players to experience any lag.

Once we scroll down a bit more we see a bunch of boxes that look like they are pretty confusing. The first step is to make a command line argument for this server. In most cases it can be pretty simple, but feel free to play around with it, and check out the [command line options](https://developer.valvesoftware.com/wiki/Command_Line_Options) to see what else there is. We are going to use a very simple command.
[block:code]
{
  "codes": [
    {
      "code": "-game ${game} -strictportbind -port ${port} -console +map ${map} -maxplayers ${players} -norestart",
      "language": "text",
      "name": ""
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/rtk5ax8S5iWpOCWGzFNH",
        "Screen Shot 2015-04-24 at 10.05.00 PM.png",
        "1454",
        "366",
        "#5c97d3",
        ""
      ]
    }
  ]
}
[/block]
Those variables (e.g. `${game}`) allow Scales to dynamically apply values depending on what you change in PufferPanel. This makes it really easy to change the default map, or move the server to a new IP or Port if necessary.

After adding the command line, we need to fill out some additional required fields. The `Maximum Players` field (remember, this includes bots as well as humans), and map fields should be pretty straightforward. The `SRCDS Game` field should be the name of the game that you are installing and a full list of these games [can be found here](http://forums.srcds.com/viewtopic/12473). For this example we will be using `insurgency`. The next field is the `SRCDS Application ID` which [can be found here](https://developer.valvesoftware.com/wiki/Dedicated_Servers_List) and differers for each game type. For Insurgency, it would be `237410`.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/6bYUUIV2S7qT5JgUt6h5",
        "zLKNd.png",
        "1472",
        "478",
        "#db5f4d",
        ""
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "We will be ignoring the `Additional Parameters` field for this tutorial, you can leave it blank."
}
[/block]
After filling out those fields, click the button to generate a SFTP password, and then press create server. This will create the server on the desired node, and then you will be directed to the server information in the panel. Upon being redirected you will have access to the installer console which will display a live feed of the install process. We suggest keeping this window open in the background while it runs so you can monitor it. The install process is completely automatic and your server will be available in the panel once it is completed.
[block:image]
{
  "images": [
    {
      "image": [],
      "caption": "Example output from the installer window."
    }
  ]
}
[/block]
Congratulations! You are the new owner of a Source Dedicated Server run through PufferPanel.