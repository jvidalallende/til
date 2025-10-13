# RDS requires two availability zones

When deploying an RDS database, even when using the development type and single AZ,
RDS forces us to create a subnet group that has subnets in two different AZs.

From [AWS documentation][00] (emphasis mine):

_A DB subnet group is a collection of subnets (typically private) that you create in a VPC and that
you then designate for your DB instances. [...]
Each DB subnet group should **have subnets in at least two Availability Zones** in a given AWS Region._

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets
