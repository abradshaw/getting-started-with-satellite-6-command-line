# Activation Keys

```
hammer activation-key create --name "RHEL65-Activation-Key-2" \
--content-view "RHEL65-content-view-1" \
--lifecycle-environment Library --organization "Example Org"
Activation key created

hammer activation-key update --release-version "6.5"  \
--organization "Example Org" --name "RHEL65-Activation-Key-1"
Activation key updated
```

Now the key is created but needs additional configuration such as adding **Subscriptions**

This step requires some interim steps to find the **IDs** we need. First step is to list the available **Subscriptions**

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





