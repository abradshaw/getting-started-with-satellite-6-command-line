# Defining Content Views

Once the repositories that we need are syncronised, we can get our content view created. The content view will create a frozen view of the repositories until further updates are added to it and published.

OK, lets remind ourself of the IDs of our syncronised repositories, as its simpler to define the repositories we want to add to our **content view**, by ID

Again, to simplify cut and paste, lets define another variable

```
CV1="RHEL65-Content_View"
```


```
hammer repository list --organization "${ORG}"

---|-----------------------------------------------------------------|-----------
ID | NAME                                                            | CONTENT TYPE
---|-----------------------------------------------------------------|-----------
1  | Red Hat Enterprise Linux 6 Server Kickstart x86_64 6Server      | yum
3  | Red Hat Enterprise Linux 6 Server - RH Common RPMs x86_64       | yum
2  | Red Hat Enterprise Linux 6 Server RPMs x86_64 6Server           | yum
---|-----------------------------------------------------------------|-----------

```

Lets create our **content view** now, called **RHEL65-Content_View**


```
hammer content-view create --name "${CV1}" \
 --description "Our initial first content view" \
 --organization "${ORG}"
```

Next we add the repositories to the **content view**

```
hammer content-view update --repository-ids 1,2,3 \
--name "RHEL65-Content_View" --organization "${ORG}"
```

Finally we can publish our **content view**

```
hammer content-view publish --name "${CV1}" \
--organization "${ORG}"
```

**NOTE:** Its possible to also add the ```--async``` to this publish command if required
