<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
 </style>

# Activation Keys

Activation keys are required, when registering the host, in order to apply the correct settings to the host

<div class=warn>**NOTE** Unfortunatley the version of subscription manager shipped in RHEL6.5 (and below) does not function correctly with Activation Keys. The default **subscription_manager_registration** snippet has a fix to ensure that the RH Common repo is included, so that provisioning should work fine.
RHEL6.6 and RHEL7 do work correctly.
</div>

**NOTE:** We need to wait for our **content view** to publish and have an activation key created, before we continue

```
hammer activation-key create --name "RHEL65-Activation-Key-1" \
--content-view "RHEL65-content-view-1" \
--lifecycle-environment Library --organization "Example Org"
Activation key created
```
If you are not using **6Server** channels, its critical to set the release version on the key. Even if you are, its probably better to do so
```
hammer activation-key update --release-version "6.5"  \
--organization "Example Org" --name "RHEL65-Activation-Key-1"
Activation key updated
```

Now the key is created but needs additional configuration such as adding **Subscriptions**

This step requires some interim steps to find the **IDs** we need. First step is to list the available **Subscriptions**. We need the **ID** (the last but one column)

```
hammer subscription list --organization "Example Org"
```

We also need to list the **activation keys** as we need the **ID** from that also

```
hammer activation-key list --organization "Example Org"
```

Then using the result from the **ID** columns, attach the subscription

```
hammer activation-key add-subscription --id <activation key ID> \
--subscription-id <subscription ID>

```





