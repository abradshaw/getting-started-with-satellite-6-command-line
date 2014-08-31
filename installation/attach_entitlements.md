<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
 </style>

# Attach Entitlements

OK, lets get a list of whats availble to you, you are specifically looking for the **Pool IDs** here

`subscription-manager list --available --all|less`

Search for the Satellite Subscription, as a Red Hat employee, some of the output I see is as follows, yours will look a little different

```
Subscription Name: Red Hat Satellite Employee Subscription
Provides:          Red Hat Beta
                   Red Hat Satellite Tools 6 MDP
                   Red Hat Satellite 6 MDP
                   Red Hat Satellite Capsule 6 Beta
                   Red Hat Enterprise Linux 7 Release Candidate
                   Red Hat Satellite 6 Beta
                   Red Hat Enterprise Linux High Availability (for RHEL Server)
                   Red Hat Enterprise Linux Server
                   Red Hat Satellite
                   Red Hat Enterprise Linux Load Balancer (for RHEL Server)
SKU:               SER0232US
Pool ID:           8a85f9873f77744e013f8944aab067cf
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

```subscription-manager attach --pool=8a85f9873f77744e013f8944aab067cf```

<div class=warn>**NOTE**:
If you get an error that reads like this

<pre>
Too many content sets for certificate Red Hat Satellite Employee Subscription.
A newer client may be available to address this problem.
See kbase https://access.redhat.com/knowledge/node/129003 for more information.
</pre>

then make sure you log on to Red Hat and select the verison of Satellite, as mentioned in the previous section. Be sure to click the update button
</div>

You will then be able to attach to that pool. However, depending on your entitlemenmts, the pool you have atached to may not have **Software Collections**. If this is the case, use subscription manager to list all availble pools and attach one that contains **Software Collections**



This may enable too many repositories. The [Satellite documentation](https://access.redhat.com/documentation/en-US/Red_Hat_Satellite/6.0/html-single/Installation_Guide/index.html#Installing_Red_Hat_Satellite) makes clear which repositories you will need, and shows how to disable the ones you dont.


```
subscription-manager repos --disable "*"

subscription-manager repos --enable rhel-6-server-rpms \
--enable rhel-server-rhscl-6-rpms \
--enable rhel-server-6-satellite-6-beta-rpms
```

Once done, check that you have access to **exactly** three repos

```
# yum repolist
...

repo id                                 repo name                                                              status
rhel-6-server-rpms                      Red Hat Enterprise Linux 6 Server (RPMs)                               12,833
rhel-server-6-satellite-6-beta-rpms     Red Hat Satellite 6.0 Beta (for RHEL 6 Server) (RPMs)                     334
rhel-server-rhscl-6-rpms                Red Hat Software Collections RPMs for Red Hat Enterprise Linux 6 Server 1,267
```

Once you have confirmed that you have access to eactly those three repositories, carry on to the next part
