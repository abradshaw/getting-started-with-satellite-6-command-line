# Adding Red Hat Repositories

OK, once the manifest is imported we can look at enabling the Red Hat repositories to be downloaded to the Satellite server

The hammer command for enabling these Red Hat repositories is

```hammer repository-set  ```

There are a large number of repositories available, as can be seen by doing

```
hammer repository-set  list --product "Red Hat Enterprise Linux Server" \
--organization  "${ORG}"
```

To get us started we shall only enable three Red Hat repositories - these are enough to enable us to perform provisioning

### Example RHEL 6 Channels
```
# hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 6 Server (Kickstart)" \
 --releasever "6.5" --basearch "x86_64"

# hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 6 Server (RPMs)" \
 --releasever "6.5" --basearch "x86_64"

# hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 6 Server - RH Common (RPMs)" \
 --basearch "x86_64"
```
### Example RHEL 7 Channels
```
hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 7 Server (Kickstart)" \
 --releasever "7.0" --basearch "x86_64"

hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 7 Server (RPMs)" \
 --releasever "7.0" --basearch "x86_64"

hammer repository-set enable  --organization "${ORG}" \
 --product "Red Hat Enterprise Linux Server" \
 --name "Red Hat Enterprise Linux 7 Server - RH Common (RPMs)" \
 --releasever "7.0" --basearch "x86_64"```

>**NOTE**:
In Satellite 6.1, you will need to add the Satellite Tools repository and the RH Common repository can be removed (unless you use it for other things like the rhevm-guest-agent, in which case you will need both)

So now you have enabled s few repositories, but they are not syncronised. See the next section for this
