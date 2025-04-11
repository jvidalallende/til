# Domain-based firewall rules require connection establishment

This was found when trying to implement a stateful firewall that only allows traffic to certain domains
(and denies all other traffic). Using a default action that dropped all traffic did also prevent reaching
domains in the allow list.

I was using domain lists, so I had not read the [document about suricata rule evaluation order][00].
After doing so, and switching the default policy to only drop established connections, the firewall worked
as expected.

After reading again the document about [stateful rule group domain names][01], it gives a hint about the need
for connection establishment, as the host header (HTTP) or SNI (HTTPS) are only present in packets after the
TCP handshake has been done:

_For HTTPS traffic, Network Firewall uses the **Server Name Indication (SNI)** extension in the TLS handshake
to determine the hostname, or domain name, that the client is trying to connect to. For HTTP traffic,
Network Firewall uses the **HTTP host header** to get the name. In both cases, Network Firewall doesn't pause
connections to do out-of-band DNS lookups. It uses the SNI or host header, not the IP addresses, when evaluating
domain list rule groups._

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://docs.aws.amazon.com/network-firewall/latest/developerguide/suricata-rule-evaluation-order.html
[01]: https://docs.aws.amazon.com/network-firewall/latest/developerguide/stateful-rule-groups-domain-names.html
