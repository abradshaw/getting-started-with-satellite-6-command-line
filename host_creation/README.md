# Host Creation

OK so we are finally ready to create our first host to be provisioned. A quick look at the options and we can make our first attempt

```
hammer host create --help| less
Usage:
    hammer host create [OPTIONS]

Options:
    --architecture ARCHITECTURE_NAME Architecture name
    --architecture-id ARCHITECTURE_ID
    --ask-root-password ASK_ROOT_PW One of true/false, yes/no, 1/0.
    --build BUILD                 One of true/false, yes/no, 1/0.
                                  Default: "true"
    --compute-attributes COMPUTE_ATTRS Compute resource attributes.
                                  Comma-separated list of key=value.
    --compute-profile COMPUTE_PROFILE_NAME Name to search by
    --compute-profile-id COMPUTE_PROFILE_ID
    --compute-resource COMPUTE_RESOURCE_NAME Compute resource name
    --compute-resource-id COMPUTE_RESOURCE
    --domain DOMAIN_NAME          Domain name
    --domain-id DOMAIN_ID
    --enabled ENABLED             One of true/false, yes/no, 1/0.
                                  Default: "true"
    --environment ENVIRONMENT_NAME Environment name
    --environment-id ENVIRONMENT_ID
    --hostgroup HOSTGROUP_NAME    Hostgroup name
    --hostgroup-id HOSTGROUP_ID
    --image-id IMAGE_ID
    --interface INTERFACE         Interface parameters.
                                  Comma-separated list of key=value.
                                  Can be specified multiple times.
    --ip IP                       not required if using a subnet with dhcp proxy
    --mac MAC                     not required if its a virtual machine
```

So lets give it a try


```
hammer host create --hostgroup "DC North"  --name "test"
Could not create the host:
  MAC address is invalid
  MAC address can't be blank
```

Right so we certainly need to set the MAC address, lets also set the domain

```
hammer host create --hostgroup "DC North"  --name "test" --mac "aa:bb:cc:dd:ee:ff"  --domain "example.com"
Host created

```

OK, looks good but we havent specified a **location** or **organisation** as it seems its not possible at creation timeor indeed after, I have opened this [bug](https://bugzilla.redhat.com/show_bug.cgi?id=1153034)



