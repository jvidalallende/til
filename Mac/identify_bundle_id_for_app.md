# Identify the bundle ID of an application

Some MacOS CLI commands are targeted to specific applications via their bundle ID.
To identify it, the easiest way via CLI is to use this command:

```
codesign -dr - /path/to/yourapp.app
```

There are other ways, see [here][00]


[//]: # ( ------------------- references below this line ------------------- )

[00]: https://stackoverflow.com/questions/39972335/how-do-i-press-and-hold-a-key-and-have-it-repeat-in-vscode
