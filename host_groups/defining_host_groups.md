# Defining Host Groups

This page has been entirely re-written in the update to 6.1, nearly all of the work arounds are now not required thankfully.

```
hammer hostgroup create --help
Usage:
    hammer host create [OPTIONS]

Options:
 --architecture ARCHITECTURE_NAME                       Architecture name
 --architecture-id ARCHITECTURE_ID                       
 --ask-root-password ASK_ROOT_PW                        One of true/false, yes/no, 1/0.
 --build BUILD                                          One of true/false, yes/no, 1/0.
                                                        Default: "true"
 --comment COMMENT                                      Additional information about this host
 --compute-attributes COMPUTE_ATTRS                     Compute resource attributes.
                                                        Comma-separated list of key=value.
 --compute-profile COMPUTE_PROFILE_NAME                 Name to search by
 --compute-profile-id COMPUTE_PROFILE_ID                 
 --compute-resource COMPUTE_RESOURCE_NAME               Compute resource name
 --compute-resource-id COMPUTE_RESOURCE_ID               
 --domain DOMAIN_NAME                                   Domain name
 --domain-id DOMAIN_ID                                  Numerical ID or domain name
 --enabled ENABLED                                      One of true/false, yes/no, 1/0.
                                                        Default: "true"
 --environment ENVIRONMENT_NAME                         Environment name
 --environment-id ENVIRONMENT_ID                         
 --hostgroup HOSTGROUP_NAME                             Hostgroup name
 --hostgroup-id HOSTGROUP_ID                             
 --image IMAGE_NAME                                     Name to search by
 --image-id IMAGE_ID                                     
 --interface INTERFACE                                  Interface parameters.
                                                        Comma-separated list of key=value.
                                                        Can be specified multiple times.
 --ip IP                                                not required if using a subnet with DHCP proxy
 --location LOCATION_NAME                               Location name
 --location-id LOCATION_ID                               
 --mac MAC                                              required for managed host that is bare metal, not required if it's a
                                                        virtual machine
 --managed MANAGED                                      One of true/false, yes/no, 1/0.
                                                        Default: "true"
 --medium MEDIUM_NAME                                   Medium name
 --medium-id MEDIUM_ID                                   
 --model MODEL_NAME                                     Model name
 --model-id MODEL_ID                                     
 --name NAME                                             
 --operatingsystem OPERATINGSYSTEM_TITLE                Operating system title
 --operatingsystem-id OPERATINGSYSTEM_ID                 
 --organization ORGANIZATION_NAME                       Organisation name
 --organization-id ORGANIZATION_ID                      organization ID
 --owner OWNER_LOGIN                                    Login of the owner
 --owner-id OWNER_ID                                    ID of the owner
 --owner-type OWNER_TYPE                                Host's owner type
                                                        Possible value(s): 'User', 'Usergroup'
 --parameters PARAMS                                    Host parameters.
                                                        Comma-separated list of key=value.

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