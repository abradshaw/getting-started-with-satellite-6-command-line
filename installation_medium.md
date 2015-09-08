# Installation Media

Next item to address is the fact that the installation media currently doent have your location/organisation set correctly

In order to take care of this, get a list of *installation media*

```
hammer medium list
```
 
Make of note of the ID of the media you want to edit

Next list the organisations and locations again, making note of the IDs

```
hammer organization list
hammer location list
```

Set the info correctly 

```
hammer location add-medium --id 4  --medium-id 7
hammer organization add-medium --id 3  --medium-id 7
```

