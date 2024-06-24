# Considering Conversational AI Latency and Jitter Requirements in the Context of Dual Queue Networking

## Background

Recently, artificial intelligence (AI) has advanced to the point that conversational AI (C-AI) has become computationally possible. But C-AI only works 
acceptably for end users when network and computational delay is within acceptable bounds to make C-AI interactions feel like a normal conversation with 
another human being. However, the tech industry has been almost entirely focused on the computational advancements required to make this possible. That is certainly 
understanable, since until C-AI became practicable from the perspective of compute power, no other factors mattered. 

Now that C-AI is possible due to compuational advancements, the other factors affective QoE come into view. If we put aside human factors like the pace and intonation 
of voice responses, a primary factor directly affecting QoE is network performance. They key network factors are working latency (delay) and jitter (variation of 
delay). Luckily, the network industry has been working on forms of low latency networking for some time, with new Active Queue Management (AQM) algorithms having 
been deployed over the last several years that dramatically lowers latency and jitter under normal working conditions (https://arxiv.org/abs/2107.13968).

In addition, and more intriguingly, the IETF has standardized Low Latency, Low Loss, Scalable Throughput (L4S) 
(https://www.rfc-editor.org/rfc/rfc9330.html, https://www.rfc-editor.org/rfc/rfc9331.html, https://www.rfc-editor.org/rfc/rfc9332.html). L4S provides for two 
distinct network queues at likely bottleneck links - such as in the home network gateway and ISP access network. This network technology is currently in field 
trials in the Comcast network and is expected to be deployed in production soon 
(https://corporate.comcast.com/stories/comcast-kicks-off-industrys-first-low-latency-docsis-field-trials). This technology has also been demonstrated in 5G 
and other types of access network (https://www.bell-labs.com/research-innovation/projects-and-initiatives/l4s/).

For a good example of why network technology advances must be deployed to make C-AI usable at scale, look at demonstration videos such as this one - where the 
demo uses a phone that is connected to the local network via USB-C-based Ethernet connection rather than via Wi-Fi (https://www.youtube.com/shorts/itnmSY41krs). 
It is also unclear what the upstream connection is - whether it is to an enterprise-grade fiber network or via consumer ISP. In any case, asking end 
users to connect their phone via a wired connection to use C-AI will obviously not work - you need a network that can support this natively. 

# Components of Network Delay 

Nokia developed a very informative chart showing the components of delay and their variability. ![Nokia-Latency](https://github.com/jlivingood/IETF-L4S-Deployment/assets/8984861/d7142472-7936-4eb2-9031-804b32679cdb)

As you can see - propagation delay (e.g., speed of light over the distance to the destination - the physical layer 1) and interface delay (associated with access technologies like DOCSIS, 5G, EPON, and Wi-Fi - the link layer 2) are first and tend to be fairly well bound. But queuing delay is significant - this is the 
delay that is now being called working latency or network responsiveness. This queuing delay is what needs to be controlled in order for C-AI to become 
usable for the mass of end users. That delay occurs as bottleneck links on the end-to-end path, such as in the home network, in the customer premises equipment 
(CPE) connecting to the Internet Service Provider (ISP), and in the next hop or two within the ISP's network - where traffic is aggregated. 

While propagation and interface delays are important - they tens to be measured in tens of milliseconds or perhaps as much as 200 ms. But queuing delay is 
far more significant and far more variable - running from tens of milliseconds to whole seconds. And that is *per round trip* - and most interactions 
on the internet take several round trips. Thus, those queuing delays can grow very quickly and significant impact user QoE. 

## Network Requirements for High Quality Conversational AI

The requirements can be broken down into two areas: working latency and jitter. That is - network delay and how consisent (or variable) that delay is for end users. 

But what is an acceptable range for this delay? Fortunately, the ITU and many other organizations have studied how delay affects perceived voice conversation 
quality, because this has been a key peformance metric for voice telephony for decades. As noted in a recent paper from the Broadband Internet Technical Advisory 
Group (BITAG), *Latency Explained* (https://bitag.org/documents/BITAG_latency_explained.pdf), round-trip delay of 400 ms is the upper bound of acceptability and 
far better is 200 ms of round-trip delay. 

A recent paper from Microsoft begins to delve into how network delay affects C-AI, *The LLM Latency Guidebook: Optimizing Response Times for GenAI Applications* (https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/the-llm-latency-guidebook-optimizing-response-times-for-genai/ba-p/4131994). Using that paper - 
if we assume that loading the user's spoken prompt into the Large Language Model (LLM) and generating the response takes a total of 14 ms, then we have 386 ms of 
"budget" for network round trip latency. 

Unfortunately, many users routinely experience working latency well in excess of 386 ms. So how can networks and application developers work together to reduce and tightly control network delay?

### Move Compute Close to Users, A La CDNs

One well-tested way to combat propagation delay is to follow the path laid down by Content Delivery Networks (CDNs) - which is to place servers one hop away from 
ISP networks and to deploy into all of the major cities of the country. This eliminates the need to backhaul traffic across national backbones, with the associated speed of light delays - which is typically between 60 - 100 milliseconds (ms).

Many ISPs are also discussing "edge compute" where servers would be deployed directly into their access networks, typically at or one hop away from major 
points of aggregation. For example, in a DOCSIS network, this could be next to the Cable Modem Termination System (CMTS) to which end user cable modems connect. 

As a guideline for the purposes of this analysis, let's assume that the round-trip latency between an ISP peering edge and locally-interconnected 
compute servers (akin to CDN servers) is 10 ms. That leaves us with a remaining delay budget of 376 ms.

### Working Latency (a.k.a. Network Responsiveness)

TBC

### Jitter 

TBC

## Can Dual Queue Networking Deliver High C-AI QoE?

TBC

## Comparison of Network Technologies and High CA-I QoE

|            | Idle Latency | p99 Working Latency | RPMs | Jitter | Latency Budget Consumed | Projected QoE |
|------------|--------------|---------------------|------|--------|-------------------------|---------------|
| DOCSIS AQM |              |                     |      |        |                         |               |
| LL DOCSIS  |              |                     |      |        |                         |               |
| 5G FWA     |              |                     |      |        |                         |               |
| 5G Mobile  |              |                     |      |        |                         |               |
| DSL        |              |                     |      |        |                         |               |
| LEO        |              |                     |      |        |                         |               |
| PON        |              |                     |      |        |                         |               |

TBC

## Next Steps

TBC

