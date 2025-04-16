# Clone over HTTPs with token auth in Gitlab

As seen on [Stack Overflow][00], use a fixed `oauth2` username in the url, and the token as password.

If the token is saved to `.gitlab-token`, this command will do the trick:

```
git clone https://oauth2:$(cat .gitlab-token)@<your-gitlab.com/foo/bar.git>
```

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://stackoverflow.com/a/29570677
