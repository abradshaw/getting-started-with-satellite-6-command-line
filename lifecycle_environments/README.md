# Lifecycle Environments

Satellite 6 has the concept of **Lifecycle Environments**. These should generally match the names of your tiers, such as **Crash,** **Development,** **QA,** **Production** etc etc

The idea is that your hosts or clients will exist in one of these tiers. A **Content View** describing how the host should be configured is defined and pushed or **promoted** to the first tier (Crash in our example) where it is tested and refined before it is promoted to the next environment for the next team to test.

We will discuss **Content Views** in more detail in a later section

For now lets go ahead and create the four **Lifecycle Environments** mentioned above


```
hammer lifecycle-environment create --name "Engineering" \
--description "For Engineering" --organization "${ORG}" \
--prior "Library"

hammer lifecycle-environment create --name "Development" \
--description "Initial testing for the App guys" \
--organization "${ORG}" --prior "Engineering"

hammer lifecycle-environment create --name "QA" \
--description "QA testing for the App guys" \
--organization "${ORG}" --prior "Development"

hammer lifecycle-environment create --name "Production" \
--description "Production Environment" \
--organization "${ORG}" --prior "QA"
```
