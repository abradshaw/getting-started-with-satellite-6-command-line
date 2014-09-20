# Partition Tables

Check that your **Partition Table* is associated with your **Operating System**. This should have been done during the initial configuration, but when you create your own, custom ones, dont forget this step

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

Get some more info

```
hammer partition-table info --id 7
Id:                7
Name:              Kickstart default
OS Family:         Redhat
Operating systems:
    RedHat 6.5
Created at:        2014/09/11 18:41:32
Updated at:        2014/09/11 18:41:32

```
