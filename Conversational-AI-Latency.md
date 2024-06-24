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

## Network Requirements for High Quality Conversational AI

The requirements can be broken down into two areas: working latency and jitter. That is - network delay and how consisent (or variable) that delay is for end users. 
One way to combat this is to follow the path laid down by Content Delivery Networks (CDNs) - which is to place servers one hop away from ISP networks and to deploy 
into all of the major cities of the country. This eliminates the need to backhaul traffic across national backbones, with the associated speed of light delays - 
which is typically between 60 - 100 milliseconds (ms).

But what is an acceptable range for this delay? Fortunately, the ITU and many other organizations have studied how delay affects perceived voice conversation 
quality, because this has been a key peformance metric for voice telephony for decades. As noted in a recent paper from the Broadband Internet Technical Advisory 
Group (BITAG), 

### Working Latency (a.k.a. Network Responsiveness)

### Jitter 

## Can Dual Queue Networking Deliver High C-AI QoE?

## Next Steps

