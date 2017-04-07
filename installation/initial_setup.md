# Initial Setup

The **katello-installer** is used to perform the initial setup and any future changes to the existing config. Its a puppet based installation and so can be re-run without overiding the previous settings.

We will create an "all-in-one" deployment, meaning that the Satellite will have the additional roles of TFTP proxy, DHCP server and DNS server added at install time.

The Satellite has 2 network interfaces and does not forward packets between them \(to simulate a corporate firewall\).

* the network "default" is the outside link \(to sync repos\)
* the network "SatTesting" is where DNS, DHCP and PXE are handled by the Satellite

```
# provided you put your CA cert and the signed cert of the Satellite there
# otgerwise skip this and drop the cert options when installing
cd /root/SSL-cert
katello-certs-check \
  -c 2016-06-17.crt \
  -r 2016-06-17.csr \
  -k 2016-06-17_unencrypted.key \
  -b pcfe-CA-pem.crt

cd /root/SSL-cert # provided you put your CA cert and the signed cert of rthe Satellite there
satellite-installer --scenario satellite \
  --foreman-initial-organization "Sat Test" \
  --foreman-initial-location "Engineering Building" \
  --foreman-proxy-dns true \
  --foreman-proxy-dns-forwarders 8.8.8.8 \
  --foreman-proxy-dns-zone sattest.example.com \
  --foreman-proxy-dns-reverse 2.168.192.in-addr.arpa \
  --foreman-proxy-dhcp true \
  --foreman-proxy-dhcp-interface eth0 \
  --foreman-proxy-dhcp-range  "192.168.2.100 192.168.2.150" \
  --foreman-proxy-dhcp-gateway 192.168.2.2 \
  --foreman-proxy-dhcp-nameservers 192.168.2.2 \
  --foreman-proxy-tftp true \
  --foreman-proxy-tftp-servername $(hostname) \
  --capsule-puppet true \
  --certs-server-cert \$(pwd)/2016-06-17.crt \
  --certs-server-cert-req \$(pwd)/2016-06-17.csr \
  --certs-server-key \$(pwd)/2016-06-17_unencrypted.key \
  --certs-server-ca-cert \$(pwd)/pcfe-CA-pem.crt
```

> **Note**: forwarders are stored in `/etc/named/options.conf` should you wish to change them later.
>
> **Note**: if you omit  `--capsule-dhcp-nameservers` then a default nameservers option will be created in the dhcp config for the satellite servers own address, meaning that the DHCP server will advertise the satellite as the DNS server. If this is not what you want, you can add something like   `--capsule-dhcp-nameservers 10.0.0.1, 10.0.0.2` to the main katello-installer options above

A full list of other katello-setup options are available via

```
katello-installer --help
```

Once the installer has finished, you should be able to login by pointing your browser to `https://<servername>` \(assuming you have made the necessary firewall changes\).

