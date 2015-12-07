
# Activation Keys

Activation keys are required, when registering the host, in order to apply the correct settings to the host

>**NOTE** Unfortunatley the version of subscription manager shipped in RHEL6.5 (and below) does not function correctly with Activation Keys. The default **subscription_manager_registration** snippet has a fix to ensure that the RH Common repo is included, so that provisioning should work fine.
RHEL6.6 and RHEL7 do work correctly.


**NOTE:** We need to wait for our **content view** to publish and have an activation key created, before we continue

Once again we will use a variable to aid copy and pasting

```
AK1="ak-rhel7-base-1"
```

```
hammer activation-key create --name "${AK1}" \
 --content-view "${CV1}" --lifecycle-environment Library \
 --organization "${ORG}"

Activation key created
```
Even when using the UI, its easy to miss this step.
```
hammer activation-key update --release-version "7Server"  \
 --organization "${ORG}" --name "${AK1}"
Activation key updated
```

Now the key is created but needs additional configuration such as adding **Subscriptions**

This step requires some interim steps to find the **IDs** we need. First step is to list the available **Subscriptions**. We need the **ID** (the last but one column)

```
hammer subscription list --organization "${ORG}"
```

We also need to list the **activation keys** as we need the **ID** from that also

```
hammer activation-key list --organization "${ORG}"
```

Then using the result from the **ID** columns, attach the subscription

```
hammer activation-key add-subscription --id <activation key ID> \
--subscription-id <subscription ID>

```

