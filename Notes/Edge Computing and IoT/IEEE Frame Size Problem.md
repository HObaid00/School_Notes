# IEEE 802.15.4 Frame Size Problem

IEEE 802.15.4 has a maximum frame size of only $127$ bytes.

After link-layer overhead and optional security headers, the space left for IPv6 can be much smaller.

A normal IPv6 header alone is $40$ bytes:

$$\Large
\text{IPv6 base header} = 40\text{ bytes}
$$

If only about $81$ bytes remain after MAC overhead, then IPv6 leaves only:

$$\Large
81 - 40 = 41\text{ bytes}
$$

for transport headers and payload.

This is why 6LoWPAN must compress headers and support fragmentation.

---

## Links

[[Edge Computing & IoT]]