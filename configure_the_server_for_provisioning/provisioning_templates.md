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

You can get a list of **Provisioning Templates** by

```
hammer template list |less
---|-------------------------------------|----------
ID | NAME                                | TYPE
---|-------------------------------------|----------
4  | AutoYaST default                    | provision
6  | AutoYaST default PXELinux           | PXELinux
5  | AutoYaST SLES default               | provision
37 | Boot disk iPXE - generic host       | iPXE
36 | Boot disk iPXE - host               | iPXE
26 | epel                                | snippet
38 | Example Satellite Kickstart Default | provision
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
---|-------------------------------------|----------

```

The two that we require for provisioning are **Kickstart default PXELinux** and **Satellite Kickstart Default**. The later brings in the **subscription_manager_registration** snippet also

