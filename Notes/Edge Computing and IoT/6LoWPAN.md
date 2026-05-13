# 6LoWPAN

**6LoWPAN** means **IPv6 over Low-Power Wireless Personal Area Networks**.

It allows IPv6 packets to be carried over constrained low-power links such as IEEE 802.15.4.

The main idea is:

$$\Large
\text{normal IPv6} + \text{adaptation layer} \rightarrow \text{IPv6 on tiny wireless frames}
$$

6LoWPAN provides:

- IPv6 header compression
- UDP header compression
- Fragmentation and reassembly
- Support for constrained link-layer addressing
- Neighbor discovery adaptations
- Integration with IP routing such as RPL

---

## Regular IP Stack vs 6LoWPAN Stack

A normal Internet stack may look like:

$$\Large
\text{HTTP} \rightarrow \text{TCP/UDP} \rightarrow \text{IP} \rightarrow \text{Ethernet}
$$

A constrained IoT stack may look like:

$$\Large
\text{CoAP} \rightarrow \text{UDP} \rightarrow \text{IPv6 with 6LoWPAN} \rightarrow \text{IEEE 802.15.4}
$$

6LoWPAN acts as an adaptation layer between IPv6 and the constrained link layer.

The goal is to keep end-to-end IP connectivity while adapting to tiny frame sizes and low-power radios.

---

## 6LoWPAN Header Compression

6LoWPAN reduces header overhead by omitting fields that can be inferred from context.

Example idea:

- If the IPv6 version is always known, it does not need to be sent.
- If addresses can be derived from link-layer addresses, parts of the IPv6 addresses can be omitted.
- If UDP ports are in a compressible range, the UDP header can be shortened.

The goal is:

$$\Large
\text{send only information that cannot be inferred}
$$

Header compression is essential because constrained links have very small frames.

---
## 6LoWPAN Fragmentation

IPv6 requires support for packets up to at least $1280$ bytes, but IEEE 802.15.4 frames are much smaller.

Therefore, 6LoWPAN may split one IPv6 packet into several link-layer fragments.

$$\Large
\text{IPv6 packet} \rightarrow \text{fragment}_1 + \text{fragment}_2 + \cdots + \text{fragment}_n
$$

The receiver reassembles the fragments into the original IPv6 packet.

Fragmentation allows compatibility with IPv6, but it is costly: losing one fragment may require retransmission or cause the whole packet to fail.

---

## 6LoWPAN Architecture

A 6LoWPAN network is often a **stub network**, meaning it connects to the wider Internet through one or more edge routers.

Common architectures:

- **Simple LoWPAN**: one edge router connects the LoWPAN to the Internet.
- **Extended LoWPAN**: multiple edge routers share a backbone link.
- **Ad hoc LoWPAN**: the LoWPAN has no route outside itself.

The edge router connects constrained wireless nodes to normal IP networks.

---

## 6LoWPAN Neighbor Discovery

Standard IPv6 Neighbor Discovery can be inefficient for constrained networks because multicast and frequent signaling are expensive.

6LoWPAN Neighbor Discovery optimizes local discovery and address registration for low-power nodes.

Important functions include:

- Prefix dissemination
- Node registration
- Address configuration
- Router discovery

The goal is to support IPv6-style operation while reducing unnecessary radio traffic.

---

## Security in 6LoWPAN

Security can be applied at multiple layers.

| Layer | Example mechanism | Protects |
|---|---|---|
| Layer 2 | IEEE 802.15.4 link-layer security | Local wireless frames |
| Layer 3 | IPsec / ESP | IP packets |
| Layer 5+ | DTLS / application security | Application communication |

Layer-2 security protects local radio links, but protection may end at the next router. End-to-end security usually needs higher-layer mechanisms.

In IoT, security design must also consider limited CPU, memory, battery, and key management.

---

## RPL Routing for 6LoWPAN

**RPL** is a routing protocol designed for low-power and lossy networks.

It organizes nodes into a **DODAG**: Destination-Oriented Directed Acyclic Graph.

Traffic often flows toward a root node, such as an edge router.

A node's **rank** represents its relative position in the routing structure. Lower rank usually means closer to the root.

Simplified idea:

$$\Large
\text{sensor node} \rightarrow \text{parent node} \rightarrow \cdots \rightarrow \text{root / edge router}
$$

RPL is useful when links are unreliable, devices are constrained, and routes must adapt over time.

---

## Links

[[Edge Computing & IoT]]