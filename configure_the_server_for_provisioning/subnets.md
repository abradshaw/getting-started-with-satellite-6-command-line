# Subnets

We need to heck that the initial configuration has created your subnet **and** that its in the correct **Organisation** and **Location**

```
hammer subnet list
---|-------------|-------------|--------------
ID | NAME        | NETWORK     | MASK
---|-------------|-------------|--------------
1  | 172.16.30.0 | 172.16.30.0 | 255.255.255.0
---|-------------|-------------|--------------

```

You can either use the **ID** or the **Name** to see if your subnet is in the correct **Organisation** and **Location**


```
hammer subnet info --id 1
Id:            1
Name:          172.16.30.0
Network:       172.16.30.0
Mask:          255.255.255.0
Priority:
DNS:           satellite6.example.com (https://satellite6.example.com:9090)
Primary DNS:   172.16.30.200
Secondary DNS: 10.0.0.9
TFTP:          satellite6.example.com (https://satellite6.example.com:9090)
DHCP:          satellite6.example.com (https://satellite6.example.com:9090)
VLAN ID:
Gateway:       172.16.30.1
From:          172.16.30.100
To:            172.16.30.150
Domains:
    example.com
Locations:
    *** Your location
Organizations:
    *** Your Organisation

```

If your subnet doesnt exist, use hammer to create it

```
hammer subnet create --help
Usage:
    hammer subnet create [OPTIONS]

Options:
    --dhcp-id DHCP_ID             DHCP Proxy to use within this subnet
    --dns-id DNS_ID               DNS Proxy to use within this subnet
    --dns-primary DNS_PRIMARY     Primary DNS for this subnet
    --dns-secondary DNS_SECONDARY Secondary DNS for this subnet
    --domain-ids DOMAIN_IDS       Domains in which this subnet is part
                                  Comma separated list of values.
    --from FROM                   Starting IP Address for IP auto suggestion
    --gateway GATEWAY             Primary DNS for this subnet
    --mask MASK                   Netmask for this subnet
    --name NAME                   Subnet name
    --network NETWORK             Subnet network
    --tftp-id TFTP_ID             TFTP Proxy to use within this subnet
    --to TO                       Ending IP Address for IP auto suggestion
    --vlanid VLANID               VLAN ID for this subnet
    -h, --help                    print help

```

If it does exist but is in the wrong **Organisation** or **Location** then use hammer to move it

```
hammer organization add-subnet --help
Usage:
    hammer organization add-subnet [OPTIONS]

Options:
    --id ID
    --name NAME                   Organization name
    --subnet SUBNET_NAME          Subnet name
    --subnet-id SUBNET_ID
    -h, --help                    print help

```

and

```
hammer location add-subnet --help
Usage:
    hammer location add-subnet [OPTIONS]

Options:
    --id ID
    --name NAME                   Location name
    --subnet SUBNET_NAME          Subnet name
    --subnet-id SUBNET_ID
    -h, --help                    print help
    ```
----

If your subnet isn't even created, then we shall have to do it manually, lets get some help

```
hammer subnet create --help
Usage:
    hammer subnet create [OPTIONS]

Options:
    --dhcp-id DHCP_ID             DHCP Proxy to use within this subnet
    --dns-id DNS_ID               DNS Proxy to use within this subnet
    --dns-primary DNS_PRIMARY     Primary DNS for this subnet
    --dns-secondary DNS_SECONDARY Secondary DNS for this subnet
    --domain-ids DOMAIN_IDS       Domains in which this subnet is part
                                  Comma separated list of values.
    --from FROM                   Starting IP Address for IP auto suggestion
    --gateway GATEWAY             Primary DNS for this subnet
    --mask MASK                   Netmask for this subnet
    --name NAME                   Subnet name
    --network NETWORK             Subnet network
    --tftp-id TFTP_ID             TFTP Proxy to use within this subnet
    --to TO                       Ending IP Address for IP auto suggestion
    --vlanid VLANID               VLAN ID for this subnet
    -h, --help                    print help

```

We will need most of these settings, we also need to know the ID of the **Capules/Smart Proxies** we installed to take care of DNS & DHCP

```
hammer proxy list
---|-----------------------------|------------------------------------------|--------------------------
ID | NAME                        | URL                                      | FEATURES
---|-----------------------------|------------------------------------------|--------------------------
1  | satellite6.example.com | https://satellite6.example.com:9090 | TFTP, DNS, DHCP, Puppe...
---|-----------------------------|------------------------------------------|--------------------------
```
We also need to verify that the **domain ID** before we create the subnet

```
hammer domain list
---|------------
ID | NAME
---|------------
1  | example.com
---|------------
```

OK, we have enough information to create the subnet

```
hammer subnet create --dhcp-id 1 --dns-id 1  \
 --dns-primary 172.16.30.250 --domain-ids 1 \
 --from "172.16.30.100" --gateway "172.16.30.1"\
 --mask "255.255.255.0" --name "172.16.30.0/24"\
 --network "172.16.30.0" --tftp-id 1 --to "172.16.30.199"
```

OK, that created the subnet, now we need to associate it with our **location** and **organisation**. The command is very similar to the one we used for our **domain** earlier. Check out the syntax

```
 hammer location add-subnet --help
Usage:
    hammer location add-subnet [OPTIONS]

Options:
    --id ID
    --name NAME                   Location name
    --subnet SUBNET_NAME          Subnet name
    --subnet-id SUBNET_ID
    -h, --help                    print help

```

So lets associate it

```
hammer organization add-subnet --name "${ORG}" --subnet "172.16.30.0/24"

hammer location add-subnet --name "${LOC}" --subnet "172.16.30.0/24"
```

Finally, lets check that every thing has worked as we expected

```
hammer subnet info --id 1
Id:            1
Name:          172.16.30.0
Network:       172.16.30.0
Mask:          255.255.255.0
Priority:
DNS:           satellite6.example.com (https://satellite6.example.com:9090)
Primary DNS:   172.16.30.200
Secondary DNS:
TFTP:          satellite6.example.com (https://satellite6.example.com:9090)
DHCP:          satellite6.example.com (https://satellite6.example.com:9090)
VLAN ID:
Gateway:       172.16.30.1
From:          172.16.30.100
To:            172.16.30.199
Domains:
    example.com
Locations:
    *** Your location
Organizations:
    *** Your organisation

```


