<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
 </style>

# Initial Setup

The **katello-installer** is used to perform the initial setup and any future changes to the existing config. Its a puppet based installation an so can be re-run without overiding the previous settings

We will create an "all-in-one" deployment, meaning that the Satellite will have the additional roles of TFTP proxy, DHCP server and DNS server added at install time

```
katello-installer  --capsule-dns true --capsule-dns-forwarders \
8.8.8.8 --capsule-dns-interface eth0 --capsule-dns-zone \
example.com --capsule-dns-reverse 30.16.172.in-addr.arpa \
--capsule-dhcp true --capsule-dhcp-interface eth0 \
--capsule-dhcp-gateway 172.16.30.1 --capsule-tftp true
```

Note: forwarders are stored in ```/etc/named/options.conf``` should you wish to change them later

A full list of other katello-setup options are available via
```
katello installer --help
```

Up until this point, the steps have been identical to the previous book, from now on they will differ as we will try to use the command line for everything.
<div class=warn>**Note** Currently, we cant do 100% from the command line, we shall occasionally need to refer to the UI
</div>
