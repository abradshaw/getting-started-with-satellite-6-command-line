# Puppet Environment - Location

Now we need to make sure that the **puppet environment** is assigned to our **location**. So lets list the environments

```
# hammer environment list
---|--------------------------------------
ID | NAME
---|--------------------------------------
2  | KT_Example_Org_Library_CV_RHEL65_Base_3
1  | production
---|--------------------------------------
```

Now to get more info about our puppet environment

```
# hammer environment info --id 2
Id:            2
Name:          KT_Example_Org_Library_CV_RHEL65_Base_3
Puppetclasses:
    access_insights_client
Locations:
    Default Location  
Organisations:
    Adrian_Inc
Created at:    2015/09/08 11:32:12
Updated at:    2015/09/08 11:32:12
```

OK, so we can see that its only in the **Default Location** right now, lets fix that

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
# hammer environment update --id 2 --location-ids 4
Environment updated   
```

All done
