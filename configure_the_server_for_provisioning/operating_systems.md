# Operating Systems

There are a number of things that need to be set on the **Operating System**

Make sure that the following items have values

* Partition tables
* Default templates:
* Architectures:
* Installation media

```
hammer os list
---|------------|--------------|-------
ID | FULL NAME  | RELEASE NAME | FAMILY
---|------------|--------------|-------
1  | RedHat 6.5 |              | Redhat
---|------------|--------------|-------
```

```
hammer os info --id 1
Id:                 1
Full name:          RedHat 6.5
Release name:
Family:             Redhat
Name:               RedHat
Major version:      6
Minor version:      5
Partition tables:

Default templates:

Architectures:
    x86_64
Installation media:
    Example_Org/Library/Red_Hat_6_Server_Kickstart_x86_64_6_5
Templates:
    Satellite Kickstart Default (provision)
Parameters:
```

The above output shows that we are missing entries for **Partition tables** and **Default Template**. In the previous section, we added a template to the list of templates but we didnt set it to be the default.

```
hammer partition-table list
---|------------------------------|----------
ID | NAME                         | OS FAMILY
---|------------------------------|----------
1  | AutoYaST entire SCSI disk    | Suse
2  | AutoYaST entire virtual disk | Suse
3  | AutoYaST LVM                 | Suse
4  | FreeBSD                      | Freebsd
5  | Jumpstart default            | Solaris
6  | Jumpstart mirrored           | Solaris
10 | Junos default fake           | Junos
7  | Kickstart default            | Redhat
9  | Preseed custom LVM           | Debian
8  | Preseed default              | Debian
---|------------------------------|----------

```

OK, we have the info we need, lets set it

```
hammer os set-default-template --id 1 --config-template-id 31

hammer os  add-ptable --id 1 --ptable-id 7
```

And a final check

```
hammer os info --id 1
Id:                 1
Full name:          RedHat 6.5
Release name:
Family:             Redhat
Name:               RedHat
Major version:      6
Minor version:      5
Partition tables:
    Kickstart default
Default templates:
    Satellite Kickstart Default (provision)
Architectures:
    x86_64
Installation media:
    Example_Org/Library/Red_Hat_6_Server_Kickstart_x86_64_6_5
Templates:
    Satellite Kickstart Default (provision)
Parameters:


```

That looks good
