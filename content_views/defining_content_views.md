# Defining Content Views

Once the repositories that we need are syncronised, we can get our content view created. The content view will create a frozen view of the repositories until further updates are added to it and published.

OK, lets remind ourself of the IDs of our syncronised repositories, as its simpler to define the repositories we want to add to our **content view**, by ID

Again, to simplify cut and paste, lets define another variable

```
CV1="cv-rhel7-base"
```


```
hammer repository list --organization "${ORG}"

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
We dont need the kickstart repo once the anaconda has provisioned the machine, so we will exclude that and incluse the others

Lets create our **content view** now, called **cv-rhel7-base**


```
hammer content-view create --name "${CV1}" \
 --description "Our initial first content view" \
 --organization "${ORG}"
```

Next we add the repositories to the **content view**

```
hammer content-view update --repository-ids 4,2,3 \
 --name "${CV1}" --organization "${ORG}"
```

Finally we can publish our **content view**

```
hammer content-view publish --name "${CV1}" \
--organization "${ORG}"
```

**NOTE:** Its possible to also add the ```--async``` to this publish command if required
