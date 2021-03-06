# Attach Entitlements

OK, lets get a list of whats availble to you, you are specifically looking for the **Pool IDs** here

```
subscription-manager list --available --all|less
```


Search for the Satellite Subscription, as a Red Hat employee, some of the output I see is as follows, yours will look a little different

```
Subscription Name: Red Hat Satellite Subscription
Provides:          Red Hat Software Collections (for RHEL Server)
                   Red Hat Satellite Capsule
                   Red Hat Satellite
                   ....

SKU:               SER---US
Pool ID:           aaaabbbbccccddddeeeeffffgggghhh
Available:         17
Suggested:         1
Service Level:     Self-Support
Service Type:      L1-L3
Multi-Entitlement: No
Ends:              01/01/22
System Type:       Physical
```

You are interested in
the **Pool ID** of the subscription

You can **attach** this to your server as follows

```
subscription-manager attach --pool=aaaabbbbccccddddeeeeffffgggghhh
```

>**NOTE**:
If you get an error that reads like this

><pre>
Too many content sets for certificate Red Hat Satellite Employee Subscription.
A newer client may be available to address this problem.
See kbase https://access.redhat.com/knowledge/node/129003 for more information.
</pre>

>then make sure you log on to Red Hat and select the verison of Satellite, as mentioned in the previous section. Be sure to click the update button


You will then be able to attach to that pool. However, depending on your entitlemenmts, the pool you have atached to may not have **Software Collections**. If this is the case, use subscription manager to list all availble pools and attach one that contains **Software Collections**



This may enable too many repositories. The [Satellite documentation](https://access.redhat.com/documentation/en/red-hat-satellite/6.2/paged/installation-guide/) makes clear which repositories you will need, and shows how to disable the ones you dont.


### RHEL 7 Repos

```
subscription-manager repos --disable "*"

subscription-manager repos --enable rhel-7-server-rpms \
--enable rhel-server-rhscl-7-rpms \
--enable rhel-7-server-satellite-6.2-rpms
```

Once done, check that you have access to **exactly** three repos

```
# yum repolist

repo id                                 repo name
rhel-7-server-rpms/7Server/x86_64       Red Hat Enterprise Linux 7 Server (RPMs)
rhel-7-server-satellite-6.2-rpms/x86_64 Red Hat Satellite 6.2 (for RHEL 7 Server) (RPMs)
rhel-server-rhscl-7-rpms/7Server/x86_64 Red Hat Software Collections RPMs for Red Hat Enterprise Linux 7 Server
```

Once you have confirmed that you have access to exactly those three repositories, carry on to the next part.

