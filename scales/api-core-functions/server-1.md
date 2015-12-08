---
title: "/server"
excerpt: "Create a new server on the system."
---
[block:parameters]
{
  "data": {
    "0-0": "**name**",
    "0-1": "The name of the server used within Scales for identification. PufferPanel uses a UUID for this.",
    "1-0": "**user**",
    "1-1": "Username to use for SFTP related operations. Ensure that this name does not exist on the system, and that it is valid for the OS.",
    "2-0": "**build**",
    "2-1": "An array of build parameters for the docker container.\n\n*io* — The block IO bandwidth allowed for this container. All containers have a default IO of 500, but it can be modified to be 10 (lowest) to 1000 (highest). Read more about it [here](https://docs.docker.com/reference/run/#block-io-bandwidth-blkio-constraint).\n\n*cpu* — The proportion of CPU cycles allocated to the container. Read more about how docker handles this [here](https://docs.docker.com/reference/run/#cpu-share-constraint).\n\n*memory* — The maximum amount of memory in megabytes that a container is allowed to use.",
    "3-0": "**startup**",
    "3-1": "The startup parameters for the given container.\n\n*command* — The command that will be appended to the plugin invocation to run the program in the container. For a minecraft server this would be something like `-Xms${memory}M -jar ${jar}` but it is very flexible and can be whatever it needs to be.\n\n*variables* — Definitions of additional variables used in the startup command. The following is a list of built-in variables that do not need to be defined: `${memory}`, `${ip}`, `${port}`. The `build_params` key is used when building the server during the install process.",
    "4-0": "**keys**",
    "4-1": "An array of authentication keys that are allowed to access and control this server as well as the specific permissions allowed for each key. A list of permissions can be found [here](doc:server-permissions).",
    "5-0": "**gameport**",
    "6-0": "**gamehost**",
    "7-0": "**plugin**",
    "7-1": "The corresponding plugin to use with this server. The plugin also lets Scales know what docker image to use.",
    "5-1": "The port to expose publicly for this service. Docker runs each instance on a default port in the container but to expose each service it must be linked to a public port and IP.",
    "6-1": "The specific IP to expose this service on."
  },
  "cols": 2,
  "rows": 8
}
[/block]