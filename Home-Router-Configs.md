In the Comcast deployment, the XB7 and XB8 wireless gateways are supported. These are devices that combine layer 2 DOCSIS cable modems and layer 3 IP home 
routers, plus a WiFi access point. This means that L4S and NQB markings are passes back and forth between the home LAN and access network. It also means that low 
latency traffic is marked as AC_VI in the 802.11 WiFi domain (above AC_BE for classic traffic). 

But many people will have their own (COAM / retail) cable modem, or may be running their XB device in "gateway" mode. In both cases this means the user will need to 
use their own IP router, which is connected to the cable modem via ethernet cable. 

For these customers, the question is how to ensure that L4S and NQB works on some level in their router. This can mean a few things. 

1. Level 1 Support: No Bleaching
The foundation for L4S and NQB is to ensure that the router DOES NOT BLEACH the ECN or DSCP header of packets coming into the router from the internet, or out of
the router from the user LAN. See details at https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/Network-Config-Guide.md. Not bleaching packets - allowing
the marks to pass end-to-end - will mean that the packets can use the low latency queue in the cable modem's upstream interface. In the downstream direction it also
enables you to move onto Level 2 below. 

2. Level 2 Support: WiFi WMM Support
A next step, beyond allowing the packet markings to pass, is using the downstream packet marks to trigger a WiFi queuing rule. There are (at least) four WMM
queues that an access point can use, with the default being AC_BE (best effort). As packets marked for L4S or NQB come downstream from the internet into the router,
the router can optimally set a WMM rule that these packets should be placed in the AC_VI queue for better latency. 

3. Level 3 Support: Dual Queue Support
The end goal is for a home router to have two queues. This is critical, as the home network is almost always a bottleneck and thus having two queues here for
L4S and NQB is critical.


Example configurations:
* OpenWrt:
- Turn on SQM - https://openwrt.org/docs/guide-user/network/traffic-shaping/sqm_configuration?s[]=ecn
- By doing so, ECN marks will pass end-to-end without bleaching. The parameters "ingress_ecn" and "egress_ecn" are on by default, allowing ECN marking.
- For NQB you need to allow DSCP-45 marks to pass in both directions. Set the parameters "squash_dscp" and "squash_ingress" to "0" to allow marking.

