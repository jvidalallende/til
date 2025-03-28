# Miracast over Infrastructure

[Miracast][00] is a protocol that allows video transmission from devices such as phones or laptops
to receivers (e.g. TV). Most android devices support this feature, often branded differently depending
on the device manufacturer.

This standard makes use of [Wi-Fi Direct][01] to create an ad-hoc encrypted wireless connection between
the device and the receiver. In some cases, this is either inconvenient (because of the extra performance
needed by devices to keep the dual connection and transmission) or just poses a potential security risk,
so there is an extension/alternative developed my microsoft, named
[Miracast over Infrastructure (MS-MICE)][02], which requires that both the device and the receiver are in the
same local network.

Although Windows10/11 supports it, and some linux like [GNOME Network Displays][03], support on Android,
as of 2025-03-28, seems lacking.


[//]: # ( ------------------- references below this line ------------------- )

[00]: https://en.wikipedia.org/wiki/Miracast
[01]: https://en.wikipedia.org/wiki/Wi-Fi_Direct
[02]: https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-mice/ab6341b7-4fc7-41fd-a74d-3fe023455482
[03]: https://www.phoronix.com/news/GNOME-Network-Displays-0.91
