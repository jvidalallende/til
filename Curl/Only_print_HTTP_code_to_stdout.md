# Only print HTTP code to stdout

Just use these command line parameters:

```
curl -o /dev/null -s -w "%{http_code}\n" <endpoint>
```

Source: [StackOverflow][00]

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://stackoverflow.com/questions/38906626/curl-to-return-http-status-code-along-with-the-response#38906765
