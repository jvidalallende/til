# Providing good error reports in bash

All credit to [Chris Siebenmann's post][00].


```bash
trap 'echo "Exit status $? at line $LINENO from: $BASH_COMMAND"' ERR
```

From the aforementioned post: _This uses three Bash features: the special `$LINENO` and
`$BASH_COMMAND` environment variables (which have the command executed just before the trap
and the line number), and the special `ERR` Bash 'trap' condition that causes your 'trap'
statement to be invoked right when 'set -e' is causing your script to fail and exit._


[//]: # ( ------------------- references below this line ------------------- )

[00]: https://utcc.utoronto.ca/~cks/space/blog/programming/BashGoodSetEReports
