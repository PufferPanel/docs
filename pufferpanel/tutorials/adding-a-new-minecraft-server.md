---
title: "Adding a new Minecraft Server"
excerpt: "Minecraft is a game about breaking and placing blocks. At first, people built structures to protect against nocturnal monsters, but as the game grew players worked together to create wonderful, imaginative things.\n\nIt can also be about adventuring with friends or watching the sun rise over a blocky ocean. It’s pretty. Brave players battle terrible things in The Nether, which is more scary than pretty. You can also visit a land of mushrooms if it sounds more like your cup of tea."
---
[block:callout]
{
  "type": "danger",
  "title": "Spigot Installation Notice",
  "body": "You must allocate at least 1024Mb of memory to a server running Spigot in order for build tools to work. If you do not do so the build will fail and you will have to manually clean up files and get things working."
}
[/block]
Begin by creating a new server and filling out the normal information at the top such as server name and owner. Allocate the server to whatever node you wish. The next step is to select `Minecraft` as the `Server Plugin`.
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
After doing this we will want to set the maximum amount of memory that this Minecraft Server can consume. For a simple vanilla server we suggest `1024` MB. You can adjust this depending on the size of the server and the number of plugins you will be running. Disk space is not currently used in Scales, so set that to `0`. You can set a CPU limit if you want, but for the sake of this tutorial we will be setting it to `0` as well.
[block:callout]
{
  "type": "warning",
  "body": "You need to install Java in order for Minecraft to run.  On Ubuntu, `apt-get install default-jre-headless` will install it."
}
[/block]

We now need to add a command line for this server. For the sake of simplicity we will be using the following command (but feel free to make it as complex as you need).
[block:code]
{
  "codes": [
    {
      "code": "-Xmx${memory}M -jar ${jar} -nogui",
      "language": "text"
    }
  ]
}
[/block]
After doing that you will be prompted with two different fields. The first one, `Server Jar Name` is pretty straightforward, and it is the name of the `.jar` file that will run the server.  The second field contains some build parameters that we can use when creating this server. Please see [the table below](#build-parameters) for arguments and examples of how to use this.
[block:callout]
{
  "type": "info",
  "body": "We will be ignoring the `Additional Parameters` field for this tutorial, you can leave it blank."
}
[/block]
After filling out those fields press create server. This will create the server on the desired node, and then you will be directed to the server information in the panel. Upon being redirected you will have access to the installer console which will display a live feed of the install process. We suggest keeping this window open in the background while it runs so you can monitor it. The install process is completely automatic and your server will be available in the panel once it is completed.

Congratulations! You are the new owner of a Minecraft Server run through PufferPanel.
[block:api-header]
{
  "type": "basic",
  "title": "Build Parameters"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "`-p`",
    "0-1": "*plugin*",
    "0-2": "The name of the plugin that you want to install. Can be `vanilla`, `spigot`, `forge`, `sponge-forge`, or `sponge` (unsupported currently).",
    "1-0": "`-s`",
    "1-1": "*sponge version*",
    "2-0": "`-f`",
    "2-1": "*forge version*",
    "3-0": "`-v`",
    "3-1": "*vanilla version*",
    "1-2": "Defaults to version `1.8-1371-2.1DEV-430`.",
    "2-2": "Defaults to version `1.8-11.14.1.1334`.",
    "3-2": "Defaults to version `1.8.4`.",
    "4-1": "*spigot version*",
    "4-2": "There is no current way to specify a version of Spigot, the latest version will be installed.",
    "h-0": "Argument",
    "h-1": "Value",
    "h-2": "Notes"
  },
  "cols": 3,
  "rows": 5
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "Vanilla",
    "h-1": "Examples",
    "h-0": "Server Type",
    "0-1": "To install a basic vanilla server of the default version you do not need to pass any arguments.\n\n`-p vanilla`\n\n`-p vanilla -v 1.8.4`",
    "1-0": "Spigot",
    "1-1": "`-p spigot`",
    "2-0": "Forge",
    "2-1": "`-p forge`\n\n`-p forge -f 1.8-11.14.1.1334`",
    "3-0": "Sponge (Forge)",
    "3-1": "`-p sponge-forge`\n\n`-p sponge-forge -s 1.8-1371-2.1DEV-430`\n\n`-p sponge-forge -f 1.8-11.14.1.1334`\n\n`-p sponge-forge -f 1.8-11.14.1.1334 -s 1.8-1371-2.1DEV-430`",
    "4-0": "Sponge (Standalone)",
    "4-1": "Unsupported at this time."
  },
  "cols": 2,
  "rows": 5
}
[/block]