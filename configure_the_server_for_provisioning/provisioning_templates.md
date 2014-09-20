<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
</style>

# Provisioning Templates

One of the changes from the beta version is that now, copies of provisioning templates are copied to your location and organisation, but they are read only copies.

This is a nice last minute change (from the beta) as editing one template no longer affects other orgs.

If you want to change one of them, then you will need to clone it

<div class=warn>**NOTE**:
At the time of writing (just after GA, hammer still had not been updated to include this functionality. If you need to clone a template, you will need to use the UI
</div>

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

