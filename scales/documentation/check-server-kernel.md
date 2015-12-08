---
title: "Check Server Kernel"
excerpt: "If you are unsure if your kernel is supported please run the commands below to get us some output we can look through to determine this."
---
This page is for helping us determine if your kernel can be supported with Docker. Please run the commands below and then provide the output to us either on the forums or in IRC. If providing information in IRC please paste it with [paste.ee](https://paste.ee).
[block:code]
{
  "codes": [
    {
      "code": "cd /tmp\n\n# Download Script\ncurl -o check.sh https://raw.githubusercontent.com/docker/docker/master/contrib/check-config.sh\n\n# Fix Permissions\nchmod +x check.sh\n\n# Run\n./check.sh",
      "language": "shell"
    }
  ]
}
[/block]
In general, if everything under the first section (`Generally Necessary`) is green and there you are probably good to go, but there are some optional things that we make use of.
[block:api-header]
{
  "type": "basic",
  "title": "Example Output"
}
[/block]
This output is from a server that can successfully run Docker containers for Scales.
[block:code]
{
  "codes": [
    {
      "code": "warning: /proc/config.gz does not exist, searching other paths for kernel config ...\ninfo: reading kernel config from /boot/config-3.13.0-66-generic ...\n\nGenerally Necessary:\n- cgroup hierarchy: properly mounted [/sys/fs/cgroup]\n- apparmor: enabled and tools installed\n- CONFIG_NAMESPACES: enabled\n- CONFIG_NET_NS: enabled\n- CONFIG_PID_NS: enabled\n- CONFIG_IPC_NS: enabled\n- CONFIG_UTS_NS: enabled\n- CONFIG_DEVPTS_MULTIPLE_INSTANCES: enabled\n- CONFIG_CGROUPS: enabled\n- CONFIG_CGROUP_CPUACCT: enabled\n- CONFIG_CGROUP_DEVICE: enabled\n- CONFIG_CGROUP_FREEZER: enabled\n- CONFIG_CGROUP_SCHED: enabled\n- CONFIG_CPUSETS: enabled\n- CONFIG_MEMCG: enabled\n- CONFIG_MACVLAN: enabled (as module)\n- CONFIG_VETH: enabled (as module)\n- CONFIG_BRIDGE: enabled (as module)\n- CONFIG_BRIDGE_NETFILTER: enabled\n- CONFIG_NF_NAT_IPV4: enabled (as module)\n- CONFIG_IP_NF_FILTER: enabled (as module)\n- CONFIG_IP_NF_TARGET_MASQUERADE: enabled (as module)\n- CONFIG_NETFILTER_XT_MATCH_ADDRTYPE: enabled (as module)\n- CONFIG_NETFILTER_XT_MATCH_CONNTRACK: enabled (as module)\n- CONFIG_NF_NAT: enabled (as module)\n- CONFIG_NF_NAT_NEEDED: enabled\n- CONFIG_POSIX_MQUEUE: enabled\n\nOptional Features:\n- CONFIG_USER_NS: enabled\n- CONFIG_MEMCG_KMEM: enabled\n- CONFIG_MEMCG_SWAP: enabled\n- CONFIG_MEMCG_SWAP_ENABLED: missing\n    (note that cgroup swap accounting is not enabled in your kernel config, you can enable it by setting boot option \"swapaccount=1\")\n- CONFIG_RESOURCE_COUNTERS: enabled\n- CONFIG_BLK_CGROUP: enabled\n- CONFIG_IOSCHED_CFQ: enabled\n- CONFIG_BLK_DEV_THROTTLING: enabled\n- CONFIG_CGROUP_PERF: enabled\n- CONFIG_CGROUP_HUGETLB: enabled\n- CONFIG_NET_CLS_CGROUP: enabled (as module)\n- CONFIG_NETPRIO_CGROUP: enabled (as module)\n- CONFIG_CFS_BANDWIDTH: enabled\n- CONFIG_FAIR_GROUP_SCHED: enabled\n- CONFIG_RT_GROUP_SCHED: missing\n- CONFIG_EXT3_FS: missing\n- CONFIG_EXT3_FS_XATTR: missing\n- CONFIG_EXT3_FS_POSIX_ACL: missing\n- CONFIG_EXT3_FS_SECURITY: missing\n    (enable these ext3 configs if you are using ext3 as backing filesystem)\n- CONFIG_EXT4_FS: enabled\n- CONFIG_EXT4_FS_POSIX_ACL: enabled\n- CONFIG_EXT4_FS_SECURITY: enabled\n- Storage Drivers:\n  - \"aufs\":\n    - CONFIG_AUFS_FS: enabled (as module)\n  - \"btrfs\":\n    - CONFIG_BTRFS_FS: enabled (as module)\n  - \"devicemapper\":\n    - CONFIG_BLK_DEV_DM: enabled\n    - CONFIG_DM_THIN_PROVISIONING: enabled (as module)\n  - \"overlay\":\n    - CONFIG_OVERLAY_FS: missing\n  - \"zfs\":\n    - /dev/zfs: missing\n    - zfs command: missing\n    - zpool command: missing",
      "language": "text"
    }
  ]
}
[/block]