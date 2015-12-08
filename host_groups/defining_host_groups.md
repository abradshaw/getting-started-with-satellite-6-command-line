# Defining Host Groups

This page has been entirely re-written in the update to 6.1, nearly all of the work arounds are now not required thankfully.

```
hammer hostgroup create --help
Usage:
    hammer hostgroup create [OPTIONS]

Options:
 --architecture ARCHITECTURE_NAME                      Architecture name
 --architecture-id ARCHITECTURE_ID                      
 --content-source-id CONTENT_SOURCE_ID                  
 --content-view CONTENT_VIEW_NAME                      Name to search by
 --content-view-id CONTENT_VIEW_ID                     content view numeric identifier
 --domain DOMAIN_NAME                                  Domain name
 --domain-id DOMAIN_ID                                 Numerical ID or domain name
 --environment ENVIRONMENT_NAME                        Environment name
 --environment-id ENVIRONMENT_ID                        
 --lifecycle-environment LIFECYCLE_ENVIRONMENT_NAME    Name to search by
 --lifecycle-environment-id LIFECYCLE_ENVIRONMENT_ID   ID of the environment
 --location-ids LOCATION_IDS                           Comma separated list of values.
 --locations LOCATION_NAMES                            Comma separated list of values.
 --medium MEDIUM_NAME                                  Medium name
 --medium-id MEDIUM_ID                                  
 --name NAME                                            
 --operatingsystem OPERATINGSYSTEM_TITLE               Operating system title
 --operatingsystem-id OPERATINGSYSTEM_ID                
 --organization-ids ORGANIZATION_IDS                   organization ID
                                                       Comma separated list of values.
 --organizations ORGANIZATION_NAMES                    Comma separated list of values.
 --parent PARENT_NAME                                  Name of parent hostgroup
 --parent-id PARENT_ID                                  
 --partition-table, --ptable PARTITION_TABLE_NAME      Partition table name
 --partition-table-id, --ptable-id PARTITION_TABLE_ID   
 --puppet-ca-proxy PUPPET_CA_PROXY_NAME                Name of puppet CA proxy
 --puppet-ca-proxy-id PUPPET_CA_PROXY_ID                
 --puppet-class-ids, --puppetclass-ids PUPPETCLASS_IDS List of puppetclass ids
                                                       Comma separated list of values.
 --puppet-classes PUPPET_CLASS_NAMES                   Comma separated list of values.
 --puppet-proxy PUPPET_PROXY_NAME                      Name of puppet proxy
 --puppet-proxy-id PUPPET_PROXY_ID                      
 --realm REALM_NAME                                    Name to search by
 --realm-id REALM_ID                                   Numerical ID or realm name
 --subnet SUBNET_NAME                                  Subnet name
 --subnet-id SUBNET_ID                                  
 -h, --help                                            print help

```

We will create a host group called **"DC North"** in the **Library** - **Lifecycle Environment**. From the previous section, we know that our **--operatingsystem-id** is **1** and the ** --partition-table** is **"Kickstart default"**

```
hammer hostgroup create --name "DC North" \  
 --architecture "x86_64" --domain "example.com"\
 --environment "KT_Example_Org_Library_cv_rhel7_base_3"\
 --medium "Example_Org/Library/Red_Hat_Server/Red_Hat_Enterprise_Linux_7_Server_Kickstart_x86_64_7_2"\
 --operatingsystem-id 1 --partition-table "Kickstart default"\
 --puppet-ca-proxy-id 1 --puppet-proxy-id 1 \
 --subnet "172.16.0.0/24" --content-source-id "1" \
 --organizations "${ORG}"  --locations "${LOC}" \
 --lifecycle-environment "Library" --content-view "${CV1}"
```

There are two things we cant do with the above command

* Set the activation key
* Set the root password

To fix the first one

```
hammer hostgroup set-parameter --hostgroup "DC North"  --name "kt_activation_keys"   --value "${AK1}"
```

Unfortunately the second one (setting the root password at the **host group** level still cant be done, although it looks like the code has been merged upstream and so is hopefully coming to Satellite soon.  

We will just live with this for now and set the root password at the **host** creation time, in the next section