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
ID | TITLE      | RELEASE NAME | FAMILY
---|------------|--------------|-------
1  | RedHat 7.2 |              | Redhat
2  | RedHat 7.1 |              | Redhat
---|------------|--------------|-------

```

```
hammer os info --id 1
Id:                 1
Title:              RedHat 7.2
Release name:       
Family:             Redhat
Name:               RedHat
Major version:      7
Minor version:      2
Partition tables:   
    Kickstart default
Default templates:  
    Kickstart default PXELinux (PXELinux)
    Kickstart default iPXE (iPXE)
    Satellite Kickstart Default (provision)
    Satellite Kickstart Default Finish (finish)
    Satellite Kickstart Default User Data (user_data)
Architectures:      

Installation media: 

Templates:          
    Kickstart default iPXE (iPXE)
    Kickstart default PXELinux (PXELinux)
    Satellite Kickstart Default (provision)
    Satellite Kickstart Default Finish (finish)
    Satellite Kickstart Default User Data (user_data)
Parameters:

```

Again, this page is much short in 6.1 as many of the additional steps required in 6.0 are no longer required
