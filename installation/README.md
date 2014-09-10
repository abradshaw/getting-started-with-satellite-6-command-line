# Installation

## Pre-Requisites

Before we start, you need

* vanilla install of RHEL. (we will be using RHEL6, but RHEL7 is also supported)
* valid entitlement for RHEL and entitlement for Satellite
* a login to access.redat.com (for creating and downloading the manifest)

### Firewall configuration

Its worth getting the firewall configured at this stage, so that we dont forget later. I shall assume a defualt firewall config exists. Configure the firewall any way you feel confortable, there is a quick option below.


```
iptables -F
iptables -I INPUT -m state --state NEW -p tcp --dport 443 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 5671 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 8140 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 9090 -j ACCEPT
iptables -I INPUT -m state --state NEW -p tcp --dport 22 -j ACCEPT
service iptables save
```

More information on what each of these ports are for can be found  in [Installation Guide Prerequisites](https://access.redhat.com/documentation/en-US/Red_Hat_Satellite/6.0/html-single/Installation_Guide/index.html#Prerequisites3)
