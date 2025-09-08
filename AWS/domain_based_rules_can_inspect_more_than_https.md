# Domain-based rules can inspect more than just HTTPS

This was found while doing experiments form `SMTP` with [implicit TLS][00], where the first
message that the client sends is a [Client hello][01]. In this case, server port was 465.

[AWS docs][02] mention that: _For HTTPS traffic, Network Firewall uses the Server Name Indication (SNI) extension
in the TLS handshake to determine the hostname, or domain name, that the client is trying to connect to._

My guess is that AWS is capable of identifying "Client Hello" messages even if they are not targeted to
standard 443 port, and this is why the connection is succeeding in this case even if targeted to port 465.


[//]: # ( ------------------- references below this line ------------------- )

[00]: https://www.rebex.net/kb/tls-ssl-explicit-implicit/
[01]: https://tls12.xargs.org/#client-hello/annotated
[02]: https://docs.aws.amazon.com/network-firewall/latest/developerguide/stateful-rule-groups-domain-names.html
