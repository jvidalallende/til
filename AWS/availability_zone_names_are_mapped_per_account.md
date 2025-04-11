# Availability zone names are mapped per account

This is explained in the [AWS Availability Zones][00] document:

_The code for an Availability Zone is its Region code followed by a letter identifier. For example,
`us-east-2a`, `us-east-2b`, and `us-east-2c` are the Availability Zones in the `us-east-2` Region._

_In our oldest Regions, we independently map Availability Zones to codes for each AWS account.
**For example, the us-east-1a Availability Zone for your account might not be the same physical
location as it is in another account.**_

_Each Availability Zone has an AZ ID, which is the same physical location in every AWS account.
An AZ ID consists of the first three letters of the Region code, followed by the number at the end of
the Region code, followed by -az, followed by a number. For example, `euw1-az1`, `euw1-az2`, and
`euw1-az3` are the AZ IDs for the Availability Zones in the `eu-west-1` Region.
For more information, see [AZ IDs][01]._

It makes a lot of sense to distribute the load between AZs, as most people tend to use the `-a` zone
first, and if needed subsequently go up in order. It's also insteresting to know that AZs actually have IDs,
because they are referred by name almost everywhere.


[//]: # ( ------------------- references below this line ------------------- )

[00]: https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-availability-zones.html
[01]: https://docs.aws.amazon.com/global-infrastructure/latest/regions/az-ids.html
