# Brew upgrade may break fish shell

After running a routine `brew upgrade` command that triggered an update of
[fish shell][00], I started having weird issues with fish-related built-in functions.

I typically have a long-standing tmux session, and use [IlanCosman/tide][01] to have
a useful shell prompt, so there could be interactions with it.

First, I was able to make `tide` work by reloading its configuration:
```
tide reload
```

Then, I came across this [bug report][02] that recommends reloading the shell (using `-i`
since my sessions were interactive):
```
exec fish -i
``` 

After doing this on all my tmux windows, the shell came back to behaving properly.

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://fishshell.com/
[01]: https://github.com/IlanCosman/tide
[02]: https://github.com/fish-shell/fish-shell/issues/11921
