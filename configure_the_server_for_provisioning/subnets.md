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
    Europe
Organizations:
    Example Org

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

