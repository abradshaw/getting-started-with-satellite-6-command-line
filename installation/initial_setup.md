# Initial Setup

The **katello-installer** is used to perform the initial setup and any future changes to the existing config. Its a puppet based installation and so can be re-run without overiding the previous settings.

We will create an "all-in-one" deployment, meaning that the Satellite will have the additional roles of TFTP proxy, DHCP server and DNS server added at install time.

```
katello-installer  --capsule-dns true --capsule-dns-forwarders \
8.8.8.8 --capsule-dns-interface eth0 --capsule-dns-zone \
example.com --capsule-dns-reverse 30.16.172.in-addr.arpa \
--capsule-dhcp true --capsule-dhcp-interface eth0 \
--capsule-dhcp-gateway 172.16.30.1 --capsule-tftp true
```

Note: forwarders are stored in ```/etc/named/options.conf``` should you wish to change them later.

A full list of other katello-setup options are available via
```
katello installer --help
```

Once the installer has finished, you should be able to login by pointing your browser to ```https://<servername>``` (assuming you have made the necessary firewall changes).

