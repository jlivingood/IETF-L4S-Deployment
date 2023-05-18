**1.	Background Reading**

Please read the IETF documents: RFC [9330](https://www.rfc-editor.org/rfc/rfc9330.html), [9331]([url](https://www.rfc-editor.org/rfc/rfc9331.html)), 
[9332]([url](https://www.rfc-editor.org/rfc/rfc9332.html)) 


**2.	ALLOW MARKING E2E**

L4S uses the ECN field of the packet header. To ensure ECN works end-to-end, be certain that your servers, routers, and any transit/CDN/other provider IS NOT altering or bleaching the ECN field.

**3.	MARK ECT(1) FOR LOW LATENCY IN YOUR APPLICATION/OS**

- Links that support L4S have two packet processing queues: a normal (classic) best efforts queue and a low latency (L4S) queue. The L4S queue can be thought of as having a shallower queue depth to better support the needs of delay-sensitive applications. 
- For an app to use the L4S queue, they must mark their packets with the ECT(1) code point. 

**4.	BE RESPONSIVE TO CONGESTION EXPERIENCED (CE) MARKING**

If a network element experiences congestion, the Congestion Experienced (CE) codepoint in the ECN header may be set. If an application detects CE, it should respond accordingly (e.g., by quickly reducing the send rate). 

**5.	DON’T MARK NON-DELAY-SENSITIVE TRAFFIC FOR L4S**

It may seem tempting to mark all traffic for L4S handling, but this will harm the experience of queue-building apps like file downloads. Also, remember that the access network priority for L4S is still best efforts and there is not more bandwidth for L4S compared to classic traffic; they share the same bandwidth and best-efforts priority.

**6.	USE A SCALABLE CONGESTION CONTROL FOR L4S FLOWS**

L4S strongly recommends the use of a scalable congestion control, such as DCTCP, TCP Prague, SCReAM, and BBRv2. See RFC 9331, Section 4.3 for more details . 

**Non-Queue-Building (NQB) in the Future:**

-	Still under development at the IETF is a plan to use DSCP-45 for NQB traffic 
-	These are for “sparse flows” that do not need much bandwidth, such as DNS lookups. Details to come once an RFC is issued. 
 
**CableLabs references:** 

[https://l4s.cablelabs.com/l4s-testing/README.html]([url](https://l4s.cablelabs.com/l4s-testing/README.html)) and 
[https://l4s.cablelabs.com/ ]([url](https://l4s.cablelabs.com/))
