# checkmk-goodies
Goodies for [checkmk](https://checkmk.com)

## Disclaimer
- It is only tested under Debian Linux (12) 'bookworm' with check_mk 2.2.
- It comes with no warranty at all!!!
- Support will be not available.

## Install a single script (e.g. gluster)
1. Download the script(s) you need to use (or clone the github-repo)
2. Put it into the folder `/usr/lib/check_mk_agent/local/` 
3. Make the script executable (0755)
4. Rescan the host in check_mk for new services

## gluster
Based on https://exchange.checkmk.com/p/gluster

It monitors gluster demons (running-state) and peers (connection state) and volumes (needed healings).
Also, the needed healings of a volume are available as a metric.

At the head of the script, you can configure some time periods and other values.

*The change to the checkmk plugin from lpwevers is motivated as follows: The plugin immediately sets the service level to 'Critical', as soon as at least one file needs to be healed.*
*However, this seems to be a normal and regular process of glusterfs - at least if you use it under proxmox, as I do - which in my observation should not immediately trigger an alert in the monitoring.*

*The 'gluster' script therefore takes over all checks (except for the quotas) from lpwevers' plugin and supplements the volume healing check with the option of first triggering a warning and then a critical alert after a certain time or a certain count of healings.*

To use this script, you have to disable lpwevers' plugin.
