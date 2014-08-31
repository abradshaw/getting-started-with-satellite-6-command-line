# Syncronising Repositories

Before we can create hosts to be provisioned, we need to syncronise the repositories that we selected in the previous section. This may take time, depending on the speed of your internet connection

Repository syncronisation is perfromed with

```hammer repository synchronize```

So in theory this should work

```
hammer repository synchronize \
--name "Red Hat Enterprise Linux 6 Server - RH Common Beta RPMs x86_64" \
--organization "Example Org"
```

However, once you have started creating content views, you may see errors due to the repository existing more than once

```
hammer repository synchronize \
--name "Red Hat Enterprise Linux 6 Server - RH Common Beta RPMs x86_64" \
--organization "Example Org"
Could not synchronize the repository:
  Error: repository found more than once
```

If we take a look at the repositories we have, we can confirm this

```
hammer repository list --organization "Example Org"
---|----------------------------------------------------------------|-------------
ID | NAME                                                           | CONTENT TYPE
---|----------------------------------------------------------------|-------------
12 | Puppet Repo 1                                                  | puppet
5  | Red Hat Enterprise Linux 6 Server Kickstart x86_64 6.5         | yum
1  | Red Hat Enterprise Linux 6 Server Kickstart x86_64 6.5         | yum
7  | Red Hat Enterprise Linux 6 Server - RH Common Beta RPMs x86_64 | yum
3  | Red Hat Enterprise Linux 6 Server - RH Common Beta RPMs x86_64 | yum
2  | Red Hat Enterprise Linux 6 Server RPMs x86_64 6.5              | yum
11 | Red Hat Enterprise Linux 6 Server RPMs x86_64 6.5              | yum
```

As a general rule, you should use the lowest ID for each duplicate and then you can syncronise via ID

```hammer repository synchronize --id 6 --organization "Example Org" ```

Unless you are happy to wait for it to finish you can also add the **--async** option to the command

```hammer repository synchronize --id 6 --organization "Example Org" --async```
