# IP Protocol Stack

The Internet protocol stack is usually described in layers.

| Layer | Example protocols | Role |
|---|---|---|
| Application | HTTP, CoAP, RTP | Application-specific communication |
| Transport | TCP, UDP, ICMP | End-to-end transport and control |
| Network | IP / IPv6 | Addressing and routing across networks |
| Data link | Ethernet MAC, IEEE 802.15.4 MAC | Local link communication |
| Physical | Ethernet PHY, radio PHY | Transmission of raw signals |

Each layer provides services to the layer above it.

A useful mental model is:

$$\Large
\text{application data} \rightarrow \text{transport segment} \rightarrow \text{IP packet} \rightarrow \text{link frame}
$$

---

## Links

[[Edge Computing & IoT]]
