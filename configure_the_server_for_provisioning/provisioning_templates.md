# Provisioning Templates

One of the changes from the beta version is that now, copies of provisioning templates are copied to your location and organisation, but they are read only copies.

This is a nice last minute change (from the beta) as editing one template no longer affects other orgs.

If you want to change one of them, then you will need to clone it

>**NOTE**:
At the time of writing (just after GA, hammer still had not been updated to include this clone functionality. If you need to clone a template, you will need to use the UI
[Bugzilla 1160292](https://bugzilla.redhat.com/show_bug.cgi?id=1160292)

You can get a list of **Provisioning Templates** by doing the following (note that this command produces paged output by defualt, so Ive used the **--per-page 9999** option)

```
hammer template list  --per-page 9999
---|---------------------------------------|----------
ID | NAME                                  | TYPE     
---|---------------------------------------|----------
5  | Alterator default                     | provision
6  | Alterator default finish              | finish   
7  | Alterator default PXELinux            | PXELinux 
34 | alterator_pkglist                     | snippet  
8  | AutoYaST default                      | provision
10 | AutoYaST default PXELinux             | PXELinux 
9  | AutoYaST SLES default                 | provision
44 | Boot disk iPXE - generic host         | Bootdisk 
43 | Boot disk iPXE - host                 | Bootdisk 
35 | epel                                  | snippet  
36 | fix_hosts                             | snippet  
11 | FreeBSD (mfsBSD) finish               | finish   
12 | FreeBSD (mfsBSD) provision            | provision
13 | FreeBSD (mfsBSD) PXELinux             | PXELinux 
37 | freeipa_register                      | snippet  
14 | Grubby default                        | script   
38 | http_proxy                            | snippet  
48 | idm_register                          | snippet  
15 | Jumpstart default                     | provision
16 | Jumpstart default finish              | finish   
17 | Jumpstart default PXEGrub             | PXEGrub  
33 | Junos default finish                  | finish   
31 | Junos default SLAX                    | provision
32 | Junos default ZTP config              | ZTP      
18 | Kickstart default                     | provision
20 | Kickstart default finish              | finish   
22 | Kickstart default iPXE                | iPXE     
21 | Kickstart default PXELinux            | PXELinux 
23 | Kickstart default user data           | user_data
39 | kickstart_networking_setup            | snippet  
19 | Kickstart RHEL default                | provision
24 | Preseed default                       | provision
25 | Preseed default finish                | finish   
27 | Preseed default iPXE                  | iPXE     
26 | Preseed default PXELinux              | PXELinux 
28 | Preseed default user data             | user_data
40 | puppet.conf                           | snippet  
4  | PXEGrub default local boot            | PXEGrub  
2  | PXELinux default local boot           | PXELinux 
3  | PXELinux default memdisk              | PXELinux 
1  | PXELinux global default               | PXELinux 
41 | redhat_register                       | snippet  
42 | saltstack_minion                      | snippet  
45 | Satellite Kickstart Default           | provision
47 | Satellite Kickstart Default Finish    | finish   
46 | Satellite Kickstart Default User Data | user_data
49 | subscription_manager_registration     | snippet  
29 | UserData default                      | user_data
30 | WAIK default PXELinux                 | PXELinux 
---|---------------------------------------|----------

```

The two that we require for provisioning are **Kickstart default PXELinux** and **Satellite Kickstart Default**. The later brings in the **subscription_manager_registration** snippet also

Lets stick with the builtin provisioning template. Lets see what we need to do.

```
hammer template info --id 45
Id:                45
Name:              Satellite Kickstart Default
Type:              provision
Operating systems:
    RedHat 7.2
    RedHat 7.1
Locations:
    Default_Location
    *** Your location
Organizations:
    Default_Organization
    *** Your organisation

```

### Associate the PXE Linux Template with the OS

The kickstart template was take care of above, now we need to make sure that the PXE template is associated with the OS correctly 

```
# hammer template info --id 21
Id:                21
Name:              Kickstart default PXELinux
Type:              PXELinux
Operating systems: 
    RedHat 7.2
    RedHat 7.1
Locations:         
    Default Location
    *** Your location
Organisations:     
    Default Organization
    *** Your organisation

```
This page is significantly short than the 6.0 one,as many of the 6.0 bugs have been resolved in 6.1
