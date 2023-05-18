This document is a guide to developers and network operators that would like to implement the IETF's Low Latency, Low Loss, Scalable Throughput (L4S) standard. 
This is a new way to handle traffic flows that are latency sensitive by creating a second network queue at bottlenecks; one for classic traffic 
and one for low latency traffic. 

See also the [Application Developer Guide](https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/App-Developer-Guide.md) and [Low Latency Deployment Design Recommendations](https://datatracker.ietf.org/doc/draft-livingood-low-latency-deployment/)

**1. Key Points**
-	Traffic marked for the low latency queue is NOT HIGHER PRIORITY than packets using the classic queue - they are both best effort
-	Traffic marked for the low latency queue is DOES NOT GET MORE BANDWIDTH than packets using the classic queue
-	There is NO BENEFIT FOR QUEUE BUILDING (QB) TRAFFIC TO BE MARKED AS NON-QUEUE-BUILDING (NQB). In fact, it may harm the performance of the QB traffic. 
-	You need a scalable congestion control in place to use L4S (via ECN marking) while that is not the case for NQB (via DSCP marking)
-	Middle mile networks, core/backbone networks, and points of interconnection need not necessarily have two queues; they just need to pass the markings.
-	Two queues are needed on the bottleneck link on an end-to-end path. That is most commonly in the home or last mile access network.

**2.	Allow End-to-End ECN Marking**

L4S uses the Explicit Congestion Notification (ECN) field of the packet header. To ensure ECN works end-to-end, be certain that your servers, routers, and any transit/CDN/other provider IS NOT altering or bleaching the ECN field.

**3. Allow DSCP-45 Across Domain (Peer) Boundaries**
- Traffic sent TO a peer network marked with DSCP value 45 MUST pass to that peer without altering or removing the DSCP 45 marking (see exception below).
- Traffic FROM peers marked with DSCP value 45 MUST be allowed to enter the network without altering or removing the DSCP 45 marking (see exception below).
- Peer marking exception: Some peer networks may use DSCP 45 for purposes other than NQB LL within their network. In these cases, the peer using DSCP 45 for other purposes is responsible for remarking on ingree and egress from their network. 
- In all cases, traffic marked DSCP 45 must still be handled as best efforts - not a higher priority that other internet traffic. 

**4. Marking for a Low Latency Queue**
If a network link supports dual queue, then to put packets into the low latency queue, one of the following must occur:
- DSCP = 45
- ECN = ECT(1)
- ECN = CE
- Or DSCP = 45 & ECT(1) or CE (both markings)

**5. In the Wireless LAN (WiFi)**
The WLAN is often a bottleneck but IEEE 802.11 packet marking and IETF marking are not easily mapped, though WMM have various queue types (i.e., AC_BE, AC_VO, AC_VI). For experimental purposes in the early phases of deployment, we therefore recommend:
- Packets marked for the low latency queue should be mapped to WMM AC_VI (which may also be shown as UP_5)
