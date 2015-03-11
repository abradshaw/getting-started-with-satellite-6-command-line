# Importing the Manifest

Earlier on we created and downloaded our manifest, now we should import it

A quick look at the help shows it should be easy

```
hammer subscription upload --help
Usage:
    hammer subscription upload [OPTIONS]

Options:
    --async                       Do not wait for the task
    --file MANIFEST               Subscription manifest file
    --organization ORGANIZATION_NAME
    --organization-id ORGANIZATION_ID Organization id
    --organization-label ORGANIZATION_LABEL
    --repository-url REPOSITORY_URL repository url
    -h, --help                    print help

```

So the following is all we need

```
hammer subscription upload --organization "${ORG}" --file <filename here>
```

>**NOTE**: At the time of writing using the organisation **name** wasnt working for me, so I had to use **--organization-id** method instead. The ID was found by doing **hammer organization list**
<br/> <br/>
 hammer subscription upload --organization-id 5 --file &lt;filename&gt;


