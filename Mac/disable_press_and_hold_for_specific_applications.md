# Disable press-and-hold for specific applications

On OSX, there is a "Press&Hold" feature which allows alternate characters to be typed on long key presses.
This is specially annoying on code editors like Visual Studio Code, even more if `vim` keybindings are used.

To disable it, run this command and restart VSCode:

```
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
```

Use the appropriate ID for the appliation that you want to prevent from using "Press&Hold".

Found on [Stack Overflow][00]

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://stackoverflow.com/questions/39972335/how-do-i-press-and-hold-a-key-and-have-it-repeat-in-vscode
