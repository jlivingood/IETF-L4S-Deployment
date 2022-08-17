---
###
# Internet-Draft Markdown Template
#
# Rename this file from draft-todo-yourname-protocol.md to get started.
# Draft name format is "draft-<yourname>-<workgroup>-<name>.md".
#
# For initial setup, you only need to edit the first block of fields.
# Only "title" needs to be changed; delete "abbrev" if your title is short.
# Any other content can be edited, but be careful not to introduce errors.
# Some fields will be set automatically during setup if they are unchanged.
#
# Don't include "-00" or "-latest" in the filename.
# Labels in the form draft-<yourname>-<workgroup>-<name>-latest are used by
# the tools to refer to the current version; see "docname" for example.
#
# This template uses kramdown-rfc: https://github.com/cabo/kramdown-rfc
# You can replace the entire file if you prefer a different format.
# Change the file extension to match the format (.xml for XML, etc...)
#
###
title: "L4S Deployment Design Recommendations"
abbrev: "L4S Deployment Design"
category: info

docname: draft-todo-yourname-protocol-latest
submissiontype: IETF  
number: 
date: 2022-07-11
consensus: true
v: 3
area: TSV
workgroup: TSV Area Working Group
keyword:
 - latency
 - buffer bloat
 - L4S
 - low latency
venue:
  group: TSVWG
  type: Working Group
  mail: tsvwg@ietf.org
  arch: https://datatracker.ietf.org/wg/tsvwg
  github: jlivingood/L4S-Deployment-Design
  latest: https://github.com/jlivingood/L4S-Deployment-Design

author:
 -
    fullname: Jason Livingood
    organization: Comcast
    email: jason_livingood@comcast.com

normative: 

informative: 
 I-D.draft-ietf-tsvwg-l4s-arch
 I-D.draft-ietf-tsvwg-aqm-dualq-coupled
 I-D.draft-ietf-tsvwg-ecn-l4s-id
 I-D.draft-ietf-tsvwg-l4sops
 I-D.draft-ietf-tsvwg-nqb
 I-D.draft-ietf-tsvwg-dscp-considerations

--- abstract

The IETF's Transport Area Working Group (TSVWG) has finalized experimental RFCs for Low Latency, Low Loss, Scalable Throughput (L4S). These documents do a good job of describing the L4S architecture and protocol but as is normal for many such standards, especially those in experimental status, certain design decisions are ultimately left to implementers. This document explores the potential implications of key deployment design decisions and makes recommendations for those decisions.

--- middle

# Introduction

The IETF's Transport Area Working Group (TSVWG) has finalized experimental RFCs for Low Latency, Low Loss, Scalable Throughput (L4S)  {{I-D.draft-ietf-tsvwg-l4s-arch}} {{I-D.draft-ietf-tsvwg-aqm-dualq-coupled}} {{I-D.draft-ietf-tsvwg-ecn-l4s-id}} {{I-D.draft-ietf-tsvwg-l4sops}} {{I-D.draft-ietf-tsvwg-nqb}} {{I-D.draft-ietf-tsvwg-dscp-considerations}}. These documents do a good job of describing the L4S architecture and protocol but as is normal for many such standards, especially those in experimental status, certain design decisions are ultimately left to implementers. 
 
 This document explores the potential implications of key deployment design decisions and makes recommendations for those decisions. In particular, there are best practices based on prior experience as a network operator that should be considered and there are network neutrality types of considerations as well. Technologies like L4S are benign on their own, but the way they are operationally implemented can determine whether they are ultimately perceived positively and adopted by the broader Internet ecosystem. That is a key issue with L4S, because the more applications developers and edge platforms that adopt it then the greater the value to end users. 

# Network Neutrality Overview
 
Network Neutrality (aka Net Neutrality, and NN hereafter) is a concept that can mean a variety of things in different countries, based on their laws and regulations. Generally speaking it has come to mean that Internet Service Providers (ISPs) should not block, throttle, or deprioritize lawful application traffic, should not engage in paid prioritization, and so on. The meaning of NN can be complex and ever changing, so the specific details are out of scope for this document. 
 
That being said, NN concerns certainly bear on the deployment of L4S by ISPs and so should be taken into account. It is also possible that there can be confusion over prioritization, provisioned end user throughput capacity, and low latency networking. As it is envisioned in the design of the protocol, the addition of a low latency packet processing queue at a network link is merely a second packet queue and does not mean that this queue is prioritized or that it has different or greater capacity from the classic queue. Thus, a low latency queue does not create a so-called "fast lane" - but there are other NN considerations in the operational impelentation.
 
# Implications of Deployment Design Decisions
 
TODO TEXT (INCL REF TO TUSSLE PAPER)
 
## Only Applications Mark Traffic
 Only applications should mark traffic, not the network. This is for several reasons:
 - According to the end-to-end principle, this function is best delegated to the edge of the network as an architectural best practice.
 - Application marking maintains the loose coupling between the application and network layers, eliminating the need for close coordination between networks and application developers.
 - Application developers know best whether their application will benefit from low latency and which aspects of their traffic flows will or will not benefit.
 - Application traffic is almost entirely encrypted, which makes it very difficult for networks to determine application protocols and to further infer which flows will benefit from low latency and which flows may be harmed because they need to build a queue. 
 - Network operators and equipement vendors attempting to infer application type and application need will always make mistakes, incorrectly classifying traffic (REF TO NOTES) and potentially negatively affecting certain flows.  
 - The pace of innovation and iteration is necessarily faster-moving at the application edge at layer 7, rather than in the network at layer 3 where there is greater standards stability and a lower rate of major changes. As a result, the application layer is best suited to such experimentation. Network operators and equipment vendors trying to infer application needs will in addition always be in a reactive mode, one step behind changes made in applications. 

## No Provider Payments
 There should be no edge provider payments for low latency marking by itself. A key point of NN sensitivity pertains to the potential gatekeeping and barrier to entry effects of payments from edge providers to ISPs for access to the low latency queue or other specialized services. This is because it can put the ISP in the role of being perceived as picking winners and losers in the application space but it can also create barriers to entry for new developers because established developers may be the only ones able to afford such payments.
 
In addition, given that low latency marking will have strong network effects, any barriers to adoption such as this should be avoided in order to maximize the value to users and the network of a low latency queue. 

## All Providers Welcome
 Any provider should be able to mark their traffic for the low latency queue, with no restrictions other than standards compliance or other reasonable and openly documented technical guidelines. This maintains the loose cross-layer coupling that is a key tenet of the Internet's architecture by eliminating or greatly reducing any need for application providers and networks to coordinate on deployment (though such coordination is normal in the early experimental phase of any deployment).
 
 As noted above, this is another example that given low latency marking will have strong network effects, any barriers to adoption such as this should be avoided in order to maximize the value to users and the network of a low latency queue. 
 
## Device Choice
 Both customer-owned and leased devices should be supported. This avoids the risk that an ISP can be perceived as preferencing their own devices, which may carry some monthly recurring fee or other cost. It also ensures the broadest possible base of adoption, driving network effects. 

## User Choice
 Users should have a mechanism to opt out or opt in to low latency networking. If low latency networking is working correctly, it seems unlikely that a user should ever want or need to turn it off. But is is also possible it may be desirable in some troubleshooting situations or even in cases where a particular application that a user depends upon has not implemented low latency networking correctly and so the user wishes to turn it off until the developer can fix the problem.
 
# Summary of Recommended Deployment Design Decisions
 
 1. Only Applications Mark Traffic: Not the network

 2. No Provider Payments: No edge provider payments for low latency marking

 3. All Providers Welcome: Any provider can mark – no restrictions other than standards compliance (or other reasonable and openly documented technical guidelines)

 4. Device Choice: Both customer-owned and leased devices supported

 5. User Choice: Customers can opt out and in 
 
# Security Considerations

This document contains no security considerations. 
 
# Privacy Considerations

This document contains no privacy considerations. 

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
