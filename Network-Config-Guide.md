This document is a guide to developers and network operators that would like to implement the IETF's Low Latency, Low Loss, Scalable Throughput (L4S) standard. 
This is a new way to handle traffic flows that are latency sensitive by creating a second network queue at bottlenecks; one for classic traffic 
and one for low latency traffic. 

See also the [Application Developer Guide](https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/App-Developer-Guide.md) and [Low Latency Deployment Design Recommendations](https://datatracker.ietf.org/doc/draft-livingood-low-latency-deployment/)

**1.	Allow End-to-End ECN Marking**

L4S uses the Explicit Congestion Notification (ECN) field of the packet header. To ensure ECN works end-to-end, be certain that your servers, routers, and any transit/CDN/other provider IS NOT altering or bleaching the ECN field.

**2. Allow 



-	To classify traffic for the low latency queue, one of the following must occur
o	DSCP = NQB, or
o	ECN = ECT(1), or
o	ECN = CE
