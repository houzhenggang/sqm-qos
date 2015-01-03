sqm-qos
=======

sqm-qos is the successor of qos-nxt and is built on similar principles. It is designed to run as part of the sqm package developped by the [CeroWRT](https://github.com/dtaht) project.

## Principles

sqm-qos leverages *HFSC* and *fq_codel* to define two queues: Priority and Regular. Priority is guaranteed 50% upload and download bandwidth while the Regular queue is guaranteed 30%. Both queue are capped to a maximum of 90% of the total bandwidth.

Packets are allocated a traffic class based on their *DSCP* flag as well as their source or destination ports. 
Currently, services given priority are as follow (please note that the *DSCP* flags take precedence if set):

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

## Prerequisites

In order to use this script you will need to have the following packages installed on your *OpenWRT* router:

- sqm-scripts.
- luci-sqm (optional).

Both packages are included as part of *CeroWRT*.

## Setup

1) Upload to router with:

```bash
scp nxt.qos root@router:/usr/lib/sqm/
scp 10-qos root@router:/etc/hotplug.d/iface/
```

2) Configure sqm as per the followig [guide](http://www.bufferbloat.net/projects/cerowrt/wiki/Setting_up_SQM_for_CeroWrt_310). Set the queue discipline to *nxt.qos* .
