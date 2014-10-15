<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
</style>

# Host Creation

<div class=warn>**Note:** Currently there is no way of creating a new host from hammer, which is dissapointing. I have opened this [bug](https://bugzilla.redhat.com/show_bug.cgi?id=1153034)

As with **host group** creation, I will add the work around (using the web UI) until the bug is fixed. Sorry
</div>

The below solution is taken directly from the  [sister book](http://gsw-satellite6.documentation.rocks/)


----
From the web UI, go to

```Hosts > New Host```

Enter the hostname (without the domain name) of your new host. The **Organisation** and **Location** fields should be correct already. Select the **Host Group** from the dropdown, most other entries will now auto populate, with the exception of **Content Source**. Select the **Content Source**

![](../images/host-newhost-1.png)

Now over on the **Network** tab, check that the **Domain** is correct (leave **Realm** empty) and paste in the MAC address of the host you are provisioning. (check that IP is auto suggetsed - if not see troubleshooting section)

Verify that, on the Operating System Tab, that **Architecture**, **Operating system**, **Media** and **Partition table** are set and hit **Submit**

After a few seconds a screen like this should appear

![](../images/host-newhost-2.png)

Now power on the host to be provisioned.

The build should progress in these distint stages

The initial Amaconda package install stage

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

Click on the **Content Host** to see more details

![](../images/hosts-contenthost-2.png)



