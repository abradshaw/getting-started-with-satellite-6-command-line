# Prepare for Manifest Import

Once the manifest has been created, we simple need to import it into our Satellite server.

However, first we must create our **Organization** and **Location**

###Organisation

The oganisation that I shall use for this book is **Example Org** and the location I shall use is **Europe**

Lets get our orgainisation created, starting off with getting some help on the syntax

```
hammer organization create  --help
Usage:
    hammer organization create [OPTIONS]

Options:
    --description DESCRIPTION     description
    --label LABEL                 unique label
    --name NAME                   name
    -h, --help                    print help

```

So its probably enough to just specify the **--name** option

```
hammer organization create  --name "Example Org"
Organization created

```
###Location

Now the location

```
hammer location create --help
Usage:
    hammer location create [OPTIONS]

Options:
    --name NAME
    -h, --help                    print help

```

OK, that also looks simple then

```
hammer location create --name "Europe"
Location created
```

Congratulations, your first hammer commands have completed successfully. Remember to make good use of the **--help** option
