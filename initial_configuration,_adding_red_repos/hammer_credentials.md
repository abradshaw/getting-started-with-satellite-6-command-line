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

With the release of GA, the setup program was changed to randomise this password. The password is dumped to the screen, once the **katello-installer** has finished.

Just incase you didnt make a note of it, it can be recovered by running

```
awk '/^ *admin_password:/ { print $2 }' \
/etc/katello-installer/answers.katello-installer.yaml
```

Once you have edited this file, it might be worth ```chmod 600```
 the config file and stripping the password from the answers file just to safe
