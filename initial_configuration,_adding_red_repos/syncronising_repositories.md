# Synchronising Repositories

Before we can create hosts to be provisioned, we need to synchronise the repositories that we selected in the previous section. This may take time, depending on the speed of your internet connection

Repository synchronisation is perfromed with

```hammer repository synchronize```

So in theory this should work

```
hammer repository synchronize --product "Red Hat Enterprise Linux Server" \ 
 --name "Red Hat Enterprise Linux 7 Server Kickstart x86_64 7.1" \ 
 --organization "${ORG}"
```

However, once you have started creating content views, you may see errors due to the repository existing more than once

```
hammer repository synchronize --product "Red Hat Enterprise Linux Server" \ 
 --name "Red Hat Enterprise Linux 7 Server Kickstart x86_64 7.1" \ 
 --organization "${ORG}"
Could not synchronize the repository:
  Error: repository found more than once
```

If we take a look at the repositories we have, we can confirm this

```
hammer repository list --organization "${ORG}"
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------
ID | NAME                                                              | PRODUCT                         | CONTENT TYPE | URL                                                                             
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------
1  | Red Hat Enterprise Linux 7 Server Kickstart x86_64 7.1            | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7.1/x86_64/kickstart          
4  | Red Hat Enterprise Linux 7 Server - RH Common RPMs x86_64 7Server | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/rh-common/os   
2  | Red Hat Enterprise Linux 7 Server RPMs x86_64 7Server             | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/os             
3  | Red Hat Satellite Tools 6.1 for RHEL 7 Server RPMs x86_64         | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/sat-tools/6....
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------

```

As a general rule, you should use the lowest ID for each duplicate and then you can synchronise via ID

```hammer repository synchronize --id 1 --organization "${ORG}" ```

Unless you are happy to wait for it to finish you can also add the **--async** option to the command

```hammer repository synchronize --id 1 --organization "${ORG}" --async```
