---
title: "Adding a new BungeeCord Server"
excerpt: "For a long time, Minecraft server owners have had a dream that encompasses a free, easy, and reliable way to connect multiple Minecraft servers together.\n\nBungeeCord is the answer to said dream. Whether you are a small server wishing to string multiple game-modes together, or the owner of the ShotBow Network, BungeeCord is the ideal solution for you. With the help of BungeeCord, you will be able to unlock your community's full potential."
---
[block:callout]
{
  "type": "info",
  "body": "This tutorial assumes that you have PufferPanel fully installed as well as a server running a Scales instance with all required BungeeCord dependencies installed."
}
[/block]
Begin by creating a new server and filling out the normal information at the top such as server name and owner. Allocate the server to whatever node you wish. The next step is to select `BungeeCord` as the `Server Plugin`.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/4PH04ioTg6x9iFVgzdLo",
        "Screen Shot 2015-04-24 at 9.59.33 PM.png",
        "1452",
        "360",
        "#5a8fc8",
        ""
      ]
    }
  ]
}
[/block]
After doing this we will want to set the maximum amount of memory that this BungeeCord Server can consume. For a simple server we suggest about `512` MB. Disk space is not currently used in Scales, so set that to `0`. You can set a CPU limit if you want, but for the sake of this tutorial we will be setting it to `0` as well.

We now need to add a command line for this server. For the sake of simplicity we will be using the following command (but feel free to make it as complex as you need): `-Xmx${memory}M -jar ${jar}`.

After doing that you will be prompted with two different fields. The first one, `BungeeCord Jar Name ` is pretty straightforward, and it is the name of the `.jar` file that will run the server.  The second field contains some build parameters that we can use when creating this server. Please see [the table below](#build-parameters) for arguments and examples of how to use this.
[block:callout]
{
  "type": "info",
  "body": "We will be ignoring the `Additional Parameters` field for this tutorial, you can leave it blank."
}
[/block]
After filling out those fields press create server. This will create the server on the desired node, and then you will be directed to the server information in the panel. Upon being redirected you will have access to the installer console which will display a live feed of the install process. We suggest keeping this window open in the background while it runs so you can monitor it. The install process is completely automatic and your server will be available in the panel once it is completed.

Congratulations! You are the new owner of a BungeeCord Server run through PufferPanel.
[block:api-header]
{
  "type": "basic",
  "title": "Build Parameters"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "`-v`",
    "0-1": "*version*",
    "0-2": "*(optional)* The build number of the version of BungeeCord to install. Defaults to the latest version. Builds can be found [here](http://ci.md-5.net/job/BungeeCord/).",
    "h-0": "Argument",
    "h-1": "Value",
    "h-2": "Notes"
  },
  "cols": 3,
  "rows": 1
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "BungeeCord",
    "h-1": "Examples",
    "h-0": "Server Type",
    "0-1": "To install a basic server of the default version you do not need to pass any arguments.\n\n`-v 1059`"
  },
  "cols": 2,
  "rows": 1
}
[/block]