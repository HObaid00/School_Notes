# IPv4 vs IPv6 Headers

The IPv6 base header is simpler than the IPv4 header, even though IPv6 addresses are longer.

IPv4 includes fields such as header checksum and fragmentation-related fields in the base header.

IPv6 simplifies the base header and moves optional functionality into extension headers.

This supports faster processing by routers because the common header is more regular.

Simplified idea:

$$\Large
\text{IPv6 base header} = \text{fixed simple core} + \text{optional extension headers}
$$

---

## Links

[[Edge Computing & IoT]]