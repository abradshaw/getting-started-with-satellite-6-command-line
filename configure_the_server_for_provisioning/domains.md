# Domains

Also verify that your first **Domain** was created by the initial configuration task

```
hammer domain list
---|------------
ID | NAME
---|------------
1  | example.com
---|------------

```

Domains can and indeed should be part of your  **location** and **organisation**, so we shall probably have to move it. We can do this with

```
hammer location add-domain --domain "example.com" --name "Europe"
```

Next the **location**

```
hammer organization add-domain --domain "example.com" --name "Example Org"
```

Finally we can verify that this has worked, using the ID we can see in step 1

```
hammer domain info --id 1
Id:            1
Name:          example.com
Description:
DNS Id:
Subnets:

Locations:
    Europe
Organizations:
    Example Org
Parameters:

Created at:    2014/09/18 17:20:41
Updated at:    2014/09/18 17:20:41
```

Make a mental note that there is no **subnet** assigned to this domain so far, we shall take care of this later
