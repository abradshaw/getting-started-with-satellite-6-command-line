# Quick Introduction to Hammer

The command line tool that is shipped with Satellite 6 is called Hammer

To get started you can examime which commands Hammer is capable of with

```hammer --help```

You will see output line this

```
Usage:
    hammer [OPTIONS] SUBCOMMAND [ARG] ...

Parameters:
    SUBCOMMAND                    subcommand
    [ARG] ...                     subcommand arguments

Subcommands:
    activation-key                Manipulate activation keys.
    architecture                  Manipulate architectures.
    capsule                       Manipulate capsule
    compute-resource              Manipulate compute resources.
    content-host                  manipulate content hosts on the server
    content-view                  Manipulate content views.
    domain                        Manipulate domains.
    environment                   Manipulate environments.
    fact                          Search facts.
    global-parameter              Manipulate global parameters.
    gpg                           manipulate GPG Key actions on the server
    host                          Manipulate hosts.
    host-collection               Manipulate host collections
    hostgroup                     Manipulate hostgroups.

...
```

To get more specific help, you can be more specific with your request

```hammer activation-key --help```

```
Usage:
    hammer activation-key [OPTIONS] SUBCOMMAND [ARG] ...

Parameters:
    SUBCOMMAND                    subcommand
    [ARG] ...                     subcommand arguments

Subcommands:
    add-host-collection           Associate a resource
    add-subscription              Add subscription
    create                        Create an activation key
    host-collections              List associated host collections
    info                          Show an activation key
    list                          List activation keys
    remove-repository             Disassociate a resource
    remove-subscription           Remove subscription
    subscriptions                 List associated subscriptions
    update                        Update an activation key

Options:
    -h, --help                    print help

```

The more specific the request, the more specific the answer

```hammer activation-key create --help```

```
Usage:
    hammer activation-key create [OPTIONS]

Options:
    --content-view CONTENT_VIEW_NAME
    --content-view-id CONTENT_VIEW_ID content view id
    --description DESCRIPTION     description
    --environment ENVIRONMENT_NAME
    --environment-id ENVIRONMENT_ID environment id
    --name NAME                   name
    --organization ORGANIZATION_NAME
    --organization-id ORGANIZATION_ID organization identifier
    --organization-label ORGANIZATION_LABEL
    --usage-limit USAGE_LIMIT     maximum number of registered content hosts, or 'unlimited'
    -h, --help                    print help

```
