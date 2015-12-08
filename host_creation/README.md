# Host Creation

Just as for the previous section, this page is now dramatically simpler, the workarounds have been removed, as in Satellite 6.1, they are no longer needed as there are many more options in **hammer host create**

```
hammer host create --help

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
                                                        Comma-separated list of key=value.
 --partition-table, --ptable PARTITION_TABLE_NAME       Partition table name
 --partition-table-id, --ptable-id PARTITION_TABLE_ID    
 --progress-report-id PROGRESS_REPORT_ID                UUID to track orchestration tasks status, GET
                                                        /api/orchestration/:UUID/tasks
 --provision-method METHOD                              Possible value(s): 'build', 'image'
 --puppet-ca-proxy PUPPET_CA_PROXY_NAME                  
 --puppet-ca-proxy-id PUPPET_CA_PROXY_ID                 
 --puppet-class-ids, --puppetclass-ids PUPPET_CLASS_IDS Comma separated list of values.
 --puppet-classes PUPPET_CLASS_NAMES                    Comma separated list of values.
 --puppet-proxy PUPPET_PROXY_NAME                        
 --puppet-proxy-id PUPPET_PROXY_ID                       
 --realm REALM_NAME                                     Name to search by
 --realm-id REALM_ID                                    Numerical ID or realm name
 --root-pass ROOT_PASS                                  required if host is managed and value is not inherited from host group or
                                                        default password in settings
 --root-password ROOT_PW                                 
 --subnet SUBNET_NAME                                   Subnet name
 --subnet-id SUBNET_ID                                   
 --volume VOLUME                                        Volume parameters
                                                        Comma-separated list of key=value.
                                                        Can be specified multiple times.
 -h, --help                                             print help

```

As also mentioned in the previous section, setting of the root password at the **host-group** level is not possible, so we will set it here at the host creation stage (we can even have it prompt us for the password, of you dont want such things in your bash history)


All we really need now, for bare metal provisioning (physical or virtual without compute resources configured) is a **mac-address**

```
hammer host create --hostgroup "DC North" --name="satellite-provision-test" \ 
 --mac "00:1a:4a:16:01:7a" --root-password "redhat00" \ 
 --organization "${ORG}" --location "${LOC}"
Host created

```
or get it to prompt us for the password
```
hammer host create --hostgroup "DC North" --name="satellite-provision-test" \ 
 --mac "00:1a:4a:16:01:7a" --ask-root-password yes \
 --organization "${ORG}" --location "${LOC}"
Enter the root password for the host: 
Host created

```


Now power on the host to be provisioned.

The build should progress in these distinct stages

The initial Anaconda package install stage

![](../images/host-stage-anaconda.png)

Next the post section will run, switching you to VT3 so that you can follow.

First it will register, via **subscription-manager**, to the Satellite

![](../images/host-stage-registered.png)

Next it will install the katello-agent

![](../images/host-stage-katelloagent.png)

This will be followed by a ```yum update```

![](../images/host-stage-update.png)

After the full update, the final install will happen, it will install **puppet**

![](../images/host-stage-install-puppet.png)

Finally, once puppet installs, it will configure puppet and inform the Satellite server that it is built

![](../images/host-stage-completed.png)

Back on the Satellite Server, under ```Hosts > All Hosts```
, you will see the new host initally has a blue A (Active) next to it. This simply means that puppet has made changes during its initial run. It will change to a green O (no changes) next time puppet runs -in about 30 mins time.

![](../images/hosts-allhosts.png)

Also on the Satellite Server, check the status of the **Content Hosts** ```Hosts > Content Hosts```  

![](../images/hosts-contenthost-1.png)

Click on the **Content Host** to see more details (*the screenshots abave and below need updating*)

![](../images/hosts-contenthost-2.png)



