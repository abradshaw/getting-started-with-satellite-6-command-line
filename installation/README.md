# Installation

## Pre-Requisites

Before we start, you need

* vanilla install of RHEL. (we will be using RHEL6, but RHEL7 is also supported)
* valid entitlement for RHEL and entitlement for Satellite
* a login to access.redat.com (for creating and downloading the manifest)

### Firewall configuration

Its worth getting the firewall configured at this stage, so that we dont forget later. I shall assume a default firewall config exists. Configure the firewall any way you feel confortable, there is a quick option below.

### RHEL 7 Firewall
RHEL 7 uses firewalld, which is new to all of us. Below are some simple steps to get the firewall setup as we need it

Start off by verifying what the default zone is

```
firewall-cmd --get-active-zones
```

You should see something like this that indicates its active zone is *public*

```
public
  interfaces: eth0
```

If the active zones list is empty, its probably because the NIC has not been assigned to a group:

```
firewall-cmd --zone=public \
 --change-interface=nicInterfaceName
```

OK, now we have verified that, lets take a look at the default rules in place

```
firewall-cmd --zone=public --list-all
...
(output omited)
```


Of course this is not what we require, so lets add in all the ports we require including the ones for the additional capsules (DNS & DHCP).


```
firewall-cmd  --permanent --zone=public  \
 --add-service=RH-Satellite-6 --add-service=dhcp \
 --add-service=dns --add-service=tftp
# 6.2 still seems to needs also 8000 TCP for foreman-proxy
# https://bugzilla.redhat.com/show_bug.cgi?id=1248665
# [root@satellite ~]# lsof -i :8000
# COMMAND  PID          USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
# ruby    2740 foreman-proxy   10u  IPv4  22409      0t0  TCP *:irdmi (LISTEN)

firewall-cmd --zone=public --add-port="8000/tcp" --permanent
```

Now run that command again.

```
firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: eth0
  sources: 
  services: RH-Satellite-6 dhcp dhcpv6-client dns ssh tftp
  ports: 
  masquerade: no
  forward-ports: 
  icmp-blocks: 
  rich rules: 
```


As I have used ```--permanent``` above, we will have to restart the firewall for this to take effect. We use ```firewall-cmd --reload``` as it will keep the existing state information.  See the man page for more details

```
firewall-cmd  --reload 
```



More information on what each of these ports are for can be found  in [Installation Guide Prerequisites](https://access.redhat.com/documentation/en-US/Red_Hat_Satellite/6.0/html-single/Installation_Guide/index.html#Prerequisites3)
