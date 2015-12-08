---
title: "Adding BungeeCord Network Servers"
excerpt: "PufferPanel requires a little bit of modification to use BungeeCord in a local setting, but it is very easy to do, and requires only a few button presses."
---
[block:callout]
{
  "type": "info",
  "body": "This guide is for your \"non-hub\" servers in your Bungee network. Your main BungeeCord server should still be set to your public server IP so people can connect to it. If you are running your servers across multiple networks please skip down to 'Cross-Network Bungee' below."
}
[/block]
Most Bungee networks run with a public facing Bungee server, and multiple other servers running on local interfaces that only Bungee can send clients to. Running your Bungee connected servers on a public IP is dangerous as there is no authentication happening, allowing malicious users easy access.

This tutorial covers how to add Bungee servers to your network without exposing them to the public. The first thing we need to do is add another IP to our Node in PufferPanel, which is required since `localhost` does not work inside docker containers (`localhost` is local to the specific container, not the physical server). 
[block:api-header]
{
  "type": "basic",
  "title": "Finding our IP"
}
[/block]
The first thing we need to do is find what IP docker containers can access, which is found by running the following command: `ifconfig docker0`. The output below is what you should see, and you're looking for the `inet addr`. As you can see below, that IP is `172.17.42.1` which we will be using for the rest of this tutorial. **Your IP may be different, adjust this tutorial accordingly!**
[block:code]
{
  "codes": [
    {
      "code": "root@ubuntu:~$ ifconfig docker0\ndocker0   Link encap:Ethernet  HWaddr 02:42:97:fc:a3:8b  \n          inet addr:172.17.42.1  Bcast:0.0.0.0  Mask:255.255.0.0\n          inet6 addr: fe80::42:97ff:fefc:a38b/64 Scope:Link\n          UP BROADCAST MULTICAST  MTU:1500  Metric:1\n          RX packets:276477 errors:0 dropped:0 overruns:0 frame:0\n          TX packets:1191939 errors:0 dropped:0 overruns:0 carrier:0\n          collisions:0 txqueuelen:0 \n          RX bytes:24443591 (24.4 MB)  TX bytes:3492254039 (3.4 GB)",
      "language": "text"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/21UYAMeERqyWnKD5lVIC",
        "j7K4p.png",
        "1438",
        "686",
        "#985096",
        ""
      ],
      "caption": "Adding a new IP address to a node."
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Add or Update Servers"
}
[/block]
Once you've added that IP, we will provision any of our Bungee network servers to that IP. A good way to think of this is that `172.17.42.1` is equivalent to `localhost` or `127.0.0.1` for our purposes. It is inaccessible to anyone outside of the server.

If you have servers that are already created and need to update the IP they are listening on to use them with BungeeCord, simply go into their page in the Admin CP and update their connection info. After doing that simply restart the server and you'll be all set.
[block:image]
{
  "images": [
    {
      "caption": "Updating an existing server to listen on our private interface.",
      "image": [
        "https://www.filepicker.io/api/file/iSeueAETCapILMhuCdc8",
        "kE0Tr.png",
        "1454",
        "1026",
        "#1c86b1",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Configure BungeeCord"
}
[/block]
Open your `config.yml` file in BungeeCord and add your new servers. In place of using `localhost:port` you will be using `172.17.42.1:port` for your servers. See the example below if you are confused.
[block:code]
{
  "codes": [
    {
      "code": "servers:\n  lobby:\n    motd: '&1Just another BungeeCord - Forced Host'\n    address: 172.17.42.1:25568\n    restricted: false\n  pvp:\n    motd: '&1Just another BungeeCord - PvP'\n    address: 172.17.42.1:25567\n    restricted: false\nlisteners:\n- query_port: 25565\n  motd: '&1Another Bungee server'\n  tab_list: GLOBAL_PING\n  query_enabled: true\n  ping_passthrough: false\n  default_server: lobby\n  bind_local_address: true\n  fallback_server: lobby\n  host: 0.0.0.0:25565\n  max_players: 100\n  tab_size: 60\n  force_default_server: false\n  forced_hosts:\n    pvp.md-5.net: pvp",
      "language": "yaml"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Cross-Network Bungee"
}
[/block]
Because of the way that BungeeCord works you will need to add some firewall rules to prevent unauthorized access to your Bungee "nodes" if you are not running your servers on the same network.

For this to work, simply bind those servers to the public IP address, and then add a firewall rule for them to deny access to everyone except your Bungee server. In the command below, replace `<ip>` with the IP of the Bungee server that will be connecting to it, and `<port>` with the port of the server that is running on the machine.
[block:code]
{
  "codes": [
    {
      "code": "iptables -A DOCKER ! -i docker0 -s <ip> -p tcp --dport <port> -j DROP",
      "language": "text"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "body": "You will most likely need to restart docker after running the above command. We're looking into ways to prevent having to do that. **You do not need to restart Scales, just docker.**"
}
[/block]