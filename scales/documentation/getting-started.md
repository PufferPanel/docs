---
title: "Getting Started"
excerpt: ""
---
[block:callout]
{
  "type": "danger",
  "title": "STOP",
  "body": "Do not install or attempt to use Scales on systems other than `Ubuntu 14.04 LTS`, `Ubuntu 15.10`, `CentOS 7.1`, or `Debian 8.2`. They are not supported."
}
[/block]
With the release of `PufferPanel 0.8.3` installing Scales has become an incredibly easy process. We now have auto-deployment scripts built into PufferPanel that allow Scales to be installed with a single command. If you would rather manually install Scales, please see the documentation for that, [found here](doc:manually-installing-scales). This page assumes that you will be using the auto-deploy feature.
[block:api-header]
{
  "type": "basic",
  "title": "Step 1: Add a Node"
}
[/block]
On your PufferPanel installation, add a new node filling everything out correctly as you go. Once you have successfully added it, move to the next step.
[block:api-header]
{
  "type": "basic",
  "title": "Step 2: Generate Script"
}
[/block]
Go to the node information page and switch to the 'Auto-Deploy' tab. There will be a button that says `Generate Auto-Deployment Script`, press it. This will update the page to look like the picture below.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/erLOB6LuSRiOjsg7yKxi",
        "mRrsB.png",
        "1434",
        "1308",
        "#c64450",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Step 3: Login to the Server and Run Script"
}
[/block]
After you have generated a script, simply SSH into the server that this node is configured for and then paste the command that is listed (`sudo bash -c 'source <(...)'`). You will be prompted about checking your kernel, **this is a very important step**.
[block:callout]
{
  "type": "info",
  "title": "Kernel Notices",
  "body": "Users who are running on OVH systems will need to update their kernel before installing Scales, documentation for that can be [found here](doc:switching-ovh-kernels). Most kernels will work fine, such as the default DigitalOcean, Linode, and Vultr kernels. If you are unsure about this step we suggest asking us on IRC or on the forums and also check out our [kernel support page](doc:check-server-kernel)."
}
[/block]
After verifying that you are using a supported kernel simply enter `y` into the prompt field and press enter. Scales will begin installing automatically, there is nothing else you need to do. If the script exits at any point before saying it was installed successfully then there was an error and you should try to provide us with those logs so we can look into the problem. You can always [install Scales manually](doc:getting-started) if needed.
[block:callout]
{
  "type": "success",
  "body": "Congratulations, Scales is now installed and running. Head back to PufferPanel and add your first server!"
}
[/block]