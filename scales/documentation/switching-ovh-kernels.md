---
title: "Switching OVH Kernels"
excerpt: "This documentation is from [Sysadmin World](http://www.sysadminworld.com/2012/how-to-switch-to-the-standard-ubuntu-kernel-on-ovh/) and is preserved here for reference."
---
[block:callout]
{
  "type": "warning",
  "body": "This documentation is only for users running OVH kernels. You can check if this is the case by running `uname -r`. If it ends with `-grsec-xxxx-grs-ipv6-64` or similar it is probably an OVH kernel. Standard Ubuntu Kernels look like `3.13.0-37-generic`."
}
[/block]
OVH default kernels are shipped without support for virtualization solutions such as Docker, KVM, Xen, etc. This makes it rather problematic to try and use Scales on these machines because we leverage Docker instances to run servers, and these instances rely on `cgroup` which helps limit CPU and IO usage.

The commands below will switch you to a default non-OVH kernel.
[block:code]
{
  "codes": [
    {
      "code": "#Update apt sources\nsudo apt-get update\n# Install standard Ubuntu Kernel\nsudo apt-get install linux-image-server || sudo apt-get install linux-image-generic\n\n# Change Boot Order\nmv /etc/grub.d/06_OVHkernel /etc/grub.d/25_OVHkernel\n\n# Update Grub\nsudo update-grub\n\n# Restart the Server\nsudo shutdown -r now",
      "language": "curl"
    }
  ]
}
[/block]
If the above commands worked, `uname -r` should output something ending with `-generic` rather than `-grsec-xxxx-grs-ipv6-64`.