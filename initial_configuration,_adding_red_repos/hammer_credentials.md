# Hammer Credentials

To run hammer you need to provide authentication, you can specify your username and password each time

```hammer -u admin -p <password> <subcommands>```

or simple edit **/etc/hammer/cli.modules.d/foreman.yml**

```
:foreman:
	:enable_module: true
	:host: 'https://localhost/'
	:username: 'admin'
	:password: '<password>'
```

Personally I find the second option much more convienient, so I shall assume you have do this for all further examples
