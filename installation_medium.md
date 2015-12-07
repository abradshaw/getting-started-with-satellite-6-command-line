# Installation Media

Next item to address is the fact that the installation media currently doent have your location/organisation set correctly

In order to take care of this, get a list of *installation media*

```
hammer medium list
```
 
Make of note of the ID of the media you want more info on


```
hammer medium info --id 7
Id:                7
Name:              Example_Org/Library/Red_Hat_Server/Red_Hat_Enterprise_Linux_7_Server_Kickstart_x86_64_7_1
Path:              http://satellite.example.com/pulp/repos/Example_Org/Library/content/dist/rhel/server/7/7.1/x86_64/kickstart/
OS Family:         Redhat
Operating systems: 
    RedHat 7.1
Organisations:     
    Example Org
Created at:        2015/12/07 10:11:21
Updated at:        2015/12/07 10:11:21

```

Looks like the organisation **is** set but the lociation isnt, so we will correct that

```
hammer location add-medium --medium-id 7 --name "${LOC}"
```

Final check

```
hammer medium info --id 7
Id:                7
Name:              Example_Org/Library/Red_Hat_Server/Red_Hat_Enterprise_Linux_7_Server_Kickstart_x86_64_7_1
Path:              http://satellite.example.com/pulp/repos/Example_Org/Library/content/dist/rhel/server/7/7.1/x86_64/kickstart/
OS Family:         Redhat
Operating systems: 
    RedHat 7.1
Locations:         
    Europe
Organisations:     
    Example Org
Created at:        2015/12/07 10:11:21
Updated at:        2015/12/07 10:11:21

```

Looks like I forgot to get the 7.2 kickstart as well, so lets add that repo and get it syncronised


```
hammer repository-set enable  --organization "${ORG}"  --product "Red Hat Enterprise Linux Server"  --name "Red Hat Enterprise Linux 7 Server (Kickstart)"  --releasever "7.2" --basearch "x86_64"
 Repository enabled

hammer repository list --organization "${ORG}"
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------
ID | NAME                                                              | PRODUCT                         | CONTENT TYPE | URL                                                                             
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------
1  | Red Hat Enterprise Linux 7 Server Kickstart x86_64 7.1            | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7.1/x86_64/kickstart          
11 | Red Hat Enterprise Linux 7 Server Kickstart x86_64 7.2            | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7.2/x86_64/kickstart          
4  | Red Hat Enterprise Linux 7 Server - RH Common RPMs x86_64 7Server | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/rh-common/os   
2  | Red Hat Enterprise Linux 7 Server RPMs x86_64 7Server             | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/os             
3  | Red Hat Satellite Tools 6.1 for RHEL 7 Server RPMs x86_64         | Red Hat Enterprise Linux Server | yum          | https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/sat-tools/6....
---|-------------------------------------------------------------------|---------------------------------|--------------|---------------------------------------------------------------------------------

hammer repository synchronize --id 11 --organization "${ORG}"

```
We will also need to add the location to this one

hammer location add-medium --medium-id 8 --name "${LOC}"

hammer medium info --id 8
Id:                8
Name:              Example_Org/Library/Red_Hat_Server/Red_Hat_Enterprise_Linux_7_Server_Kickstart_x86_64_7_2
Path:              http://satellite.example.com/pulp/repos/Example_Org/Library/content/dist/rhel/server/7/7.2/x86_64/kickstart/
OS Family:         Redhat
Operating systems: 
    RedHat 7.2
Locations:         
    Europe
Organisations:     
    Example Org
Created at:        2015/12/07 13:08:54
Updated at:        2015/12/07 13:08:54

```
