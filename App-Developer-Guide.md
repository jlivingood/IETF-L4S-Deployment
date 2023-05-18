This document is a guide to developers and network operators that would like to implement the IETF's Low Latency, Low Loss, Scalable Throughput (L4S) standard. 
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

Application Support:

-	If a flow is incorrectly marked as NQB and it uses the low latency queue but then begins to build a queue, then the Queue Protection Function (QP) will redirect the traffic to the classic queue. This is described in XXXXXX.
-	Determine whether your application needs “sparse” flows or “congestion-controlled” flows.
o	Sparse Flows are identified via DSCP marking: these are Non-Queue Building (NQB) flows for real-time interactive flows. In addition, the bandwidth need is inherently limited by the type of application. Think of flows such as console-based gaming or VoIP – these applications will be maximally limited by the particular A/V codecs or by the limited stream needed to convey player activities. In contrast to NQB, think of a file download such as an operating system update; this file will be downloaded at a rate that is unlimited by the application – it will be limited by the available bandwidth of the path to the end user. 
o	L4S Congestion Controlled Flows are identified via ECN marking: these are flows that need higher bandwidth than the spare NQB flows described above. The bandwidth is not inherently limited by the application, which means the user quality (e.g. video resolution) may improve as more and more bandwidth can be used. Think of flows such as cloud-based gaming or video conferencing. In the latter case, it is obviously latency sensitive NQB traffic but the UI will look better and better as the video quality (bandwidth consumed) ramps up – such as from SD to HD to 4K-quality video. 
![image](https://github.com/jlivingood/IETF-L4S-Deployment/assets/8984861/434c3595-8a85-4d99-ab17-989e1c12b2de)

 
 
**CableLabs references:** 

[https://l4s.cablelabs.com/l4s-testing/README.html](https://l4s.cablelabs.com/l4s-testing/README.html) and 
[https://l4s.cablelabs.com/ ](https://l4s.cablelabs.com/)
