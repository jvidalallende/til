# Using custom DNS resolvers for specific domains

This is properly explained [here][00].

In short, adding files to `/etc/resolver/<domain-name>` with the format of the
[/etc/resolv.conf][01] format makes the OS use that specific configuration for
the domain.

For example, a file named `/etc/resolver/mylab.local` with content:

```
nameserver 10.0.0.53
nameserver 10.0.0.54
```

Will resolve DNS queries to the `mylab.local` domain using those name servers.

After creating the file, force a DNS refresh with `sudo killall -HUP mDNSResponder`.
Then check the output of `scutil --dns` and verify that your domain has the
expected nameservers.

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://vninja.net/2020/02/06/macos-custom-dns-resolvers/
[01]: https://www.baeldung.com/linux/etc-resolv-conf-file
