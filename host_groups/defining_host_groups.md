# Defining Host Groups

Host groups take lots of settings

```
hammer hostgroup create --help
Usage:
    hammer hostgroup create [OPTIONS]

Options:
    --architecture ARCHITECTURE_NAME Architecture name
    --architecture-id ARCHITECTURE_ID
    --domain DOMAIN_NAME          Domain name
    --domain-id DOMAIN_ID         May be numerical id or domain name
    --environment ENVIRONMENT_NAME Environment name
    --environment-id ENVIRONMENT_ID
    --medium MEDIUM_NAME          Medium name
    --medium-id MEDIUM_ID
    --name NAME
    --operatingsystem-id OPERATINGSYSTEM_ID
    --parent-id PARENT_ID
    --ptable PTABLE_NAME          Partition table name
    --ptable-id PTABLE_ID
    --puppet-ca-proxy-id PUPPET_CA_PROXY_ID
    --puppet-proxy-id PUPPET_PROXY_ID
    --puppetclass-ids PUPPETCLASS_IDS Comma separated list of values.
    --realm REALM_NAME            Name to search by
    --realm-id REALM_ID           May be numerical id or realm name
    --subnet SUBNET_NAME          Subnet name
    --subnet-id SUBNET_ID
    -h, --help                    print help
```

We will create a host group called **"DC North"** in the **Library** - **Lifecycle Environment**. From the previous section, we know that our **--operatingsystem-id** is **1** and the ** --ptable** is **7**

```
hammer hostgroup create --name "DC North" \
--architecture "x86_64" --domain "example.com"\
--environment "KT_Example_Org_Library_RHEL65_Content_View_1_5"\
--medium "Example_Org/Library/Red_Hat_6_Server_Kickstart_x86_64_6_5"\
--operatingsystem-id 1 --ptable "Kickstart default"\
--puppet-ca-proxy-id 1 --puppet-proxy-id 1 \
--subnet "172.16.30.0/24"
```

Right away, we need to add it to to our **location** and **organisation**

```
hammer location add-hostgroup --name "Europe" --hostgroup "DC North"

hammer organization add-hostgroup --name "Example Org" --hostgroup "DC North"
```

Things missing at this point

* Content Source
* Password
* Activation Key

