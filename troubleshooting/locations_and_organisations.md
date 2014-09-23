# Locations and Organisations

These are relatively new in the development lifecycle, and while the GA is better than the beta, there is still room for improvement.

A nice way to check that we have all the elements we need in each **Location** and **Organisation** is to use the hammer command to list all info about each one

```
hammer  location list
---|-----------------
ID | NAME
---|-----------------
2  | Default_Location
9  | Europe
---|-----------------
```

```
hammer  location info --id 9
Id:                 9
Name:               Europe
Users:

Smart proxies:

Subnets:
    172.16.30.0/24 (172.16.30.0/24)
Compute resources:

Installation media:

Templates:
    freeipa_register ()
    idm_register ()
    Kickstart default iPXE (iPXE)
    Kickstart default PXELinux (PXELinux)
    puppet.conf ()
    PXELinux global default (PXELinux)
    Satellite Finish Default (finish)
    Satellite Kickstart Default (provision)
    Satellite User Data Default (user_data)
    subscription_manager_registration ()
Domains:
    Example.com
Environments:

Hostgroups:
    DC North
Parameters:

Created at:         2014/09/18 17:58:16
Updated at:         2014/09/20 16:03:21

```

The things that jump out to me above are

* missing Smart Proxies
* Missing Installation Media
* Missing (puppet) Envronments
* Missing Parameters

Next lets take a look for **organisations**

```
hammer organization list
---|----------------------|----------------------|----------------------------------
ID | NAME                 | LABEL                | DESCRIPTION
---|----------------------|----------------------|----------------------------------
1  | Default_Organization | Default_Organization | Default_Organization Organization
10 | Example Org          | Example_Org          |
---|----------------------|----------------------|----------------------------------
```

```
hammer organization info --id 10
Id:                     10
Name:                   Example Org
Users:

Smart proxies:
    sat6-hammer-test.example.com
Subnets:
    172.16.30.0/24 (172.16.30.0/24)
Compute resources:

Installation media:
    Example_Org/Library/Red_Hat_6_Server_Kickstart_x86_64_6_5
Templates:
    freeipa_register ()
    idm_register ()
    Kickstart default iPXE (iPXE)
    Kickstart default PXELinux (PXELinux)
    puppet.conf ()
    PXELinux global default (PXELinux)
    Satellite Finish Default (finish)
    Satellite Kickstart Default (provision)
    Satellite User Data Default (user_data)
    subscription_manager_registration ()
Domains:
    example.com
Environments:
    KT_Example_Org_Library_RHEL65_Content_View_1_5
Hostgroups:
    DC North
Parameters:

Created at:             2014/09/18 17:58:19
Updated at:             2014/09/20 16:03:12
Label:                  Example_Org
Description:
Red Hat Repository URL: https://cdn.redhat.com

```
