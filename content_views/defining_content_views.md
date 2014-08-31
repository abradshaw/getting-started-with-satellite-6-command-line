# Defining Content Views

Once the repositories that we need are syncronised, we can get our content view created. The content view will create a frozen view of the repositories until further updates are added to it and published.

OK, lets remind ourself of the IDs of our syncronised repositories, as its simpler to define the repositories we want to add to our **content view**, by ID

```
hammer repository list --organization "Example Org"

---|-----------------------------------------------------------------|-----------
ID | NAME                                                            | CONTENT TYPE
---|-----------------------------------------------------------------|-----------
1  | Red Hat Enterprise Linux 6 Server Kickstart x86_64 6Server      | yum
3  | Red Hat Enterprise Linux 6 Server - RH Common Beta RPMs x86_64  | yum
2  | Red Hat Enterprise Linux 6 Server RPMs x86_64 6Server           | yum
---|-----------------------------------------------------------------|-----------

```

Lets create our **content view** now, called **RHEL65-Content_View**


```
hammer content-view create --name "RHEL65-Content_View" \
--description "Our initial rhel 6.5 content view" \
--organization "Example Org"
```

Next we add the repositories to the **content view**

```
hammer content-view update --repository-ids 1,2,3 \
--name "RHEL65-Content_View" --organization "Example Org"
```

Finally we can publish our **content view**

```
hammer content-view publish --name "RHEL65-Content_View" \
--organization "Example Org"
```

**NOTE:** Its possible to also add the ```--async``` to this publish command if required
