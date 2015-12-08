---
title: "Adding Additional Port Mappings"
excerpt: "This is an advanced feature of Scales."
---
To use it, you will need to manually edit the servers config file in `/srv/scales/data/uuid.json` and add a mapping key to the build object.

In the example below if your program in the container is listening on `25565` then it is accessible to the rest of the internet by `192.168.0.8:25566`, and the port `25580` in the container is accessible by `192.168.0.8:3309`. This opens up both `tcp` and `udp` as well.
[block:code]
{
  "codes": [
    {
      "code": "\"build\": {\n    \"mapping\": {\n        \"192.168.0.8\": {\n            \"25565\": \"25566\",\n            \"25580\": \"3309\"\n        },\n        \"ip_address\": {\n            \"internal\": \"external\"\n        }\n    },\n    . . .\n}",
      "language": "text"
    }
  ]
}
[/block]
After doing that, you will need to rebuild the container from the PufferPanel Admin CP. If the server is running when you do this it will give you an error, but don't worry, you just need to restart your server and the new port bindings should take effect. If you run it while the server is stopped it should finish successfully, but if not it could just be that the process took a few seconds longer than expected. You should reference your Scales logs to determine if this is the case.

See [this GitHub issue](https://github.com/PufferPanel/Scales/issues/50) for additional discussion.