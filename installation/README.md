# Installation

## Pre-Requisites

Before we start, you need

* vanilla install of RHEL. (we will be using RHEL6, but RHEL7 is also supported)
* valid entitlement for RHEL and entitlement for Satellite
* a login to access.redat.com (for creating and downloading the manifest)

### Firewall configuration

Its worth getting the firewall configured at this stage, so that we dont forget later. I shall assume a default firewall config exists. Configure the firewall any way you feel confortable, there is a quick option below.

### RHEL 6 Firewall
```
iptables -F
iptables -I INPUT -m state --state NEW -p tcp --dport 443 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 5671 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 8140 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 9090 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 22 -j ACCEPT
# And for the Capsule services
iptables -I INPUT -m state --state NEW -p tcp --dport 53 -j ACCEPT
iptables -I INPUT -m state --state NEW -p udp --dport 53 -j ACCEPT
iptables -I INPUT -m state --state NEW -p udp --dport 67 -j ACCEPT
iptables -I INPUT -m state --state NEW -p udp --dport 68 -j ACCEPT
iptables -I INPUT -m state --state NEW -p udp --dport 69 -j ACCEPT
service iptables save
```

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

OK, now we have verified that, lets take a look at the default rules in place

```
firewall-cmd --zone=public --list-all
...
(output omited)
```


Of course this is not what we require, so lets add in all the ports we require including the ones for the additional capsules (DNS & DHCP)


```
firewall-cmd --permanent --zone=public --add-port=80/tcp \
--add-port=443/tcp  --add-port=5671/tcp --add-port=8140/tcp \
--add-port=9090/tcp --add-port=53/tcp --add-port=53/udp \
--add-port=67/udp --add-port=68/udp --add-port=69/udp
```

Now run that command again.

```
firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: eth0
  sources:
  services: dhcpv6-client ssh
  ports: 443/tcp 80/tcp 8140/tcp 9090/tcp 67/udp 68/udp 53/tcp 69/udp 53/udp 5671/tcp
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```




More information on what each of these ports are for can be found  in [Installation Guide Prerequisites](https://access.redhat.com/documentation/en-US/Red_Hat_Satellite/6.0/html-single/Installation_Guide/index.html#Prerequisites3)
