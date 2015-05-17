sqm-qos
=======

sqm-qos is the successor of qos-nxt and is built on similar principles. It is designed to run as part of the sqm package developped by the [CeroWRT](https://github.com/dtaht) project.

## Principles

sqm-qos leverages *HTB* and *fq_codel* to define two queues on egress and ingress: Priority and Regular. Priority is guaranteed 50% of the total bandwidth while the Regular queue is guaranteed 30%. Both queues are capped to a maximum of 90% of the total bandwidth.

Packets are allocated a traffic class based on their source or destination ports. The following services are given priority:

- SSH
- SMTP
- SMTPS
- DNS
- NTP
- HTTP
- HTTPS
- FTP
- IMAP
- IMAPS
- POP3
- POP3S

The traffic shaping scripts exist in two variants Routed (nxt_routed.qos) and Bridged (nxt_bridged.qos). The Routed variant makes use of iptables and connmark (ingress included with act_connmark), while the Bridged variant makes only use of tc and u32 filtering. Where applicable the Routed variant should be preferred. The bridged variant was developped, as its name suggest, for use in transparent bridge setup.

## Prerequisites

In order to use this script you will need to have the following packages installed on your *OpenWRT* router:

- sqm-scripts.
- luci-sqm (optional).

Both packages are included as part of *CeroWRT* and can be included in a custom build of *OpenWRT*.

## Setup

1) Upload to router with:

```bash
scp nxt_routed.qos root@router:/usr/lib/sqm/
```

2) Configure sqm as per the followig [guide](http://www.bufferbloat.net/projects/cerowrt/wiki/Setting_up_SQM_for_CeroWrt_310). Set the queue discipline to *nxt.qos*.
