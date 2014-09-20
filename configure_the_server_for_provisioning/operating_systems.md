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
    Kickstart default
Default templates:
    Kickstart default PXELinux (PXELinux)
    Example Satellite Kickstart Default (provision)
Architectures:
    x86_64
    x86_64
Installation media:
    Example_Org/Library/Red_Hat_6_Server_Kickstart_x86_64_6_5
Templates:
    Example Satellite Kickstart Default (provision)
    Kickstart default PXELinux (PXELinux)
    Satellite Kickstart Default (provision)
Parameters:


```

