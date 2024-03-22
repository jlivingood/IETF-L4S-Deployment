Text to use for open source project feature requests:

### Description

Add Dual Queue Low Latency Networking Support (NQB)

Please consider adding server-side support for IETF Non-Queue-Building (NQB) Per Hop Behavior (PHB) as outlined in the IETF TSVWG RFCs 9330, 9331, 9332 and https://datatracker.ietf.org/doc/draft-ietf-tsvwg-nqb/. Specifically, I would like the recursive resolver to set DSCP-45 marking in all packets sent back to users (stub resolvers) in DNS responses. This will have the benefit of marking DNS responses as suitable for placement in the low latency queue at bottleneck links supporting dual queue (such as a CMTS or Cable Modem). 

NQB marking enables latency-sensitive traffic like DNS lookups to be handled in a separate queue from classic traffic. The result is that, even when competing with significant other LAN or access network traffic from a user, that the NQB-marked traffic will get very low working latency (usually close to what is observed for idle latency). 

Comcast has tested this on resolvers in the lab as part of our low latency field trial of L4S and NQB and found it meaningfully reduced Query Response Times (QRT) under normal working conditions. 

Comcast is currently the world's first ISP trialing this in the field and anticipates it being available to millions of end users in 2024. 

### Request

Enable a new configuration parameter in the server enabling a resolver operator to turn on NQB support. That specifically will mean setting DSCP value 45 in the packet header. This configuration can either cover recursive responses or all outbound traffic from the server (there should be no downside to this). 

### Links / references

RFC 9330 https://www.rfc-editor.org/rfc/rfc9330.html
RFC 9331 https://www.rfc-editor.org/rfc/rfc9331.html
RFC 9332 https://www.rfc-editor.org/rfc/rfc9332.html
NQB PHB Draft https://datatracker.ietf.org/doc/draft-ietf-tsvwg-nqb/
Comcast explainer for app developers https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/App-Developer-Guide.md
Comcast explainer for network operators https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/Network-Config-Guide.md
Comcast field trial announcement https://corporate.comcast.com/stories/comcast-kicks-off-industrys-first-low-latency-docsis-field-trials
