This document is a guide to developers that would like to implement the IETF's Low Latency, Low Loss, Scalable Throughput (L4S) standard. 
This is a new way to handle traffic flows that are latency sensitive by creating a second network queue at bottlenecks; one for classic traffic 
and one for low latency traffic. 

See also the [Network Configuration Guide](https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/Network-Config-Guide.md) and [Low Latency Deployment Design Recommendations](https://datatracker.ietf.org/doc/draft-livingood-low-latency-deployment/)


**1.	Background Reading**

Please read the IETF documents: RFC [9330](https://www.rfc-editor.org/rfc/rfc9330.html), [9331](https://www.rfc-editor.org/rfc/rfc9331.html), 
[9332](https://www.rfc-editor.org/rfc/rfc9332.html). Apple also [released a video](https://developer.apple.com/videos/play/wwdc2022/10078/) for their 2022 Worldwide Developer's Conference that is informative. 


**2.	Allow End-to-End ECN Marking**

L4S uses the Explicit Congestion Notification (ECN) field of the packet header. To ensure ECN works end-to-end, be certain that your servers, routers, and any transit/CDN/other provider IS NOT altering or bleaching the ECN field.

**3.	MARK ECT(1) FOR LOW LATENCY IN YOUR APPLICATION/OS**

- Links that support L4S have two packet processing queues: a normal (classic) best efforts queue and a low latency (L4S) queue. The L4S queue can be thought of as having a shallower queue depth to better support the needs of delay-sensitive applications. 

- For an app to use the L4S queue, they must mark their packets with the ECT(1) code point or with the Congestion Experienced (CE) code point. 

**4.	Be Responsive to Congestion Experienced (CE) Marking**

If a network element experiences congestion, the CE code point in the ECN header should be set. If an application detects CE, it should respond accordingly (e.g., by quickly reducing the send rate). 

**5.	Don't Mark Non-Delay-Sensitive Traffic for L4S**

It may seem tempting to mark all traffic for L4S handling, but this will harm the experience of queue-building apps like file downloads. Also, remember that the network priority for L4S is still best efforts and there is not more bandwidth for L4S compared to classic traffic; they share the same bandwidth and best-efforts priority.

**6.	Use a Scalable Congestion Control for L4S Flows**

L4S strongly recommends the use of a scalable congestion control, such as DCTCP, TCP Prague, SCReAM, and BBRv2. See [RFC 9331, Section 4.3](https://www.rfc-editor.org/rfc/rfc9331#section-4.3) for more details. 


**Non-Queue-Building (NQB) in the Future:**

-	The NQB specifications are still under development at the IETF. If approved, this will specific how to use DSCP-45 for NQB traffic.

-	These are for “sparse flows” that do not need much bandwidth, such as DNS lookups. Details to come once an RFC is issued; the [current document is here](https://datatracker.ietf.org/doc/draft-ietf-tsvwg-nqb/). 
 
 
**CableLabs references:** 

[https://l4s.cablelabs.com/l4s-testing/README.html](https://l4s.cablelabs.com/l4s-testing/README.html) and 
[https://l4s.cablelabs.com/ ](https://l4s.cablelabs.com/)