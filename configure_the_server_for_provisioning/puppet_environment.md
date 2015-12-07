# Puppet Environment - Location

Now we need to make sure that the **puppet environment** is assigned to our **location**. So lets list the environments

```
hammer environment list
---|---------------------------------------
ID | NAME                                  
---|---------------------------------------
2  | KT_Example_Org_Library_cv_rhel7_base_3
1  | production                            
---|---------------------------------------

```

Now to get more info about our puppet environment

```
# hammer environment info --id 2
id:            2
Name:          KT_Example_Org_Library_cv_rhel7_base_3
Puppetclasses: 
    access_insights_client
Locations:     
    Default Location
Organisations: 
    Example Org
Created at:    2015/12/07 12:23:58
Updated at:    2015/12/07 12:23:58
```

OK, so we can see that the location isnt set (its only in the **Default Location** right now), lets fix that

```
# hammer environment update --help
Usage:
    hammer environment update [OPTIONS]

Options:
 --id ID                              
 --location-ids LOCATION_IDS         Comma separated list of values.
 --locations LOCATION_NAMES          Comma separated list of values.
 --name NAME                         Environment name
 --new-name NEW_NAME                  
 --organization-ids ORGANIZATION_IDS organization ID
                                     Comma separated list of values.
 --organizations ORGANIZATION_NAMES  Comma separated list of values.
 -h, --help                          print help

```

So that looks straighforward then 
```
# hammer environment update --id 2 --locations "${LOC}"
Environment updated   
```
Lets check

```
hammer environment info --id 2
Id:            2
Name:          KT_Example_Org_Library_cv_rhel7_base_3
Puppetclasses: 
    access_insights_client
Locations:     
    Europe
Organisations: 
    Example Org
Created at:    2015/12/07 12:23:58
Updated at:    2015/12/07 12:23:58

```
Looks good now
