---
title: "Frequently Asked Questions"
excerpt: ""
---
[block:api-header]
{
  "type": "basic",
  "title": "What is Scales? Why do I need it?"
}
[/block]
Scales is the control daemon that interacts with PufferPanel in order to create and manage your server processes. The Scales process directly runs server processes, so there is no need for additional software such as `screen` or `tmux` to keep your servers running. In addition, Scales allows us to send inputs directly to the running process, and monitor it for unexpected crashes. Because of this behavior Scales is able to immediately detect an unexpected server shutdown and restart it within milliseconds.
[block:api-header]
{
  "type": "basic",
  "title": "What is SSL and why does Scales need 'SSL Certificates'?"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "How does PufferPanel communicate with Scales?"
}
[/block]
PufferPanel uses a combination of backend CURL requests and frontend AJAX requests in order to communicate with each Scales instance to update and retrieve information. In addition, we also leverage Web Sockets which allow us to stream data in real time to the panel. Web Sockets allow us to have a live console on the page, as well as display notifications immediately if your server crashes.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/uVHwIJ60QUWqZAnGQsGV",
        "scales-pp.png",
        "592",
        "542",
        "#889eae",
        ""
      ],
      "caption": "Diagram showing how PufferPanel and Scales communicate with each other. Also includes a Bungee instance on a separate physical server communicating with MC instances on another server."
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "What is Socket.io?"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "What is Docker and why is it used?"
}
[/block]