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
---|-------------------------------------|----------
ID | NAME                                | TYPE
---|-------------------------------------|----------
4  | AutoYaST default                    | provision
6  | AutoYaST default PXELinux           | PXELinux
5  | AutoYaST SLES default               | provision
37 | Boot disk iPXE - generic host       | iPXE
36 | Boot disk iPXE - host               | iPXE
26 | epel                                | snippet
27 | fix_hosts                           | snippet
7  | FreeBSD (mfsBSD) finish             | finish
8  | FreeBSD (mfsBSD) provision          | provision
9  | FreeBSD (mfsBSD) PXELinux           | PXELinux
28 | freeipa_register                    | snippet
10 | Grubby default                      | script
29 | http_proxy                          | snippet
34 | idm_register                        | snippet
11 | Jumpstart default                   | provision
12 | Jumpstart default finish            | finish
13 | Jumpstart default PXEGrub           | PXEGrub
25 | Junos default finish                | finish
23 | Junos default SLAX                  | provision
24 | Junos default ZTP config            | ZTP
15 | Kickstart default iPXE              | iPXE
14 | Kickstart default PXELinux          | PXELinux
16 | Preseed default                     | provision
17 | Preseed default finish              | finish
19 | Preseed default iPXE                | iPXE
18 | Preseed default PXELinux            | PXELinux
20 | Preseed default user data           | user_data
30 | puppet.conf                         | snippet
3  | PXEGrub default local boot          | PXEGrub
2  | PXELinux default local boot         | PXELinux
1  | PXELinux global default             | PXELinux
33 | Satellite Finish Default            | finish
31 | Satellite Kickstart Default         | provision
32 | Satellite User Data Default         | user_data
35 | subscription_manager_registration   | snippet
21 | UserData default                    | user_data
22 | WAIK default PXELinux               | PXELinux
---|-------------------------------------|----------


```

The two that we require for provisioning are **Kickstart default PXELinux** and **Satellite Kickstart Default**. The later brings in the **subscription_manager_registration** snippet also

Lets stick with the builtin provisioning template. Lets see what we need to do.

```
hammer template info --id 31
Id:                31
Name:              Satellite Kickstart Default
Type:              provision
Operating systems:

Locations:
    Default_Location
    *** Your location
Organizations:
    Default_Organization
    *** Your organisation

```

OK we only need to make sure that it is associated with the **operating system** then. We can only specify the operating system by ID and not name, so lets get the ID

```
 hammer os list
---|------------|--------------|-------
ID | FULL NAME  | RELEASE NAME | FAMILY
---|------------|--------------|-------
1  | RedHat 6.5 |              | Redhat
---|------------|--------------|-------
```

So all we **should** need to do is

```
hammer template update --id 31 --operatingsystem-ids 1
Could not update the config template:
  This template is locked. Please clone it to a new template to customize.
```

So it seems that the GA release (6.0.4) version has a bug, and so we need to work around this like so

```
hammer os add-config-template --id 1 --config-template-id 31

hammer template info --id 31
Id:                33
Name:              Satellite Kickstart Default
Type:              provision
Operating systems:
    RedHat 6.5
Locations:
    Default_Location
    *** Your location
Organizations:
    Default_Organization
    *** Your organisation
```
