# 6LoWPAN Fragmentation

IPv6 requires support for packets up to at least $1280$ bytes, but IEEE 802.15.4 frames are much smaller.

Therefore, 6LoWPAN may split one IPv6 packet into several link-layer fragments.

$$\Large
\text{IPv6 packet} \rightarrow \text{fragment}_1 + \text{fragment}_2 + \cdots + \text{fragment}_n
$$

The receiver reassembles the fragments into the original IPv6 packet.

Fragmentation allows compatibility with IPv6, but it is costly: losing one fragment may require retransmission or cause the whole packet to fail.

---

## Links

[[Edge Computing & IoT]]
