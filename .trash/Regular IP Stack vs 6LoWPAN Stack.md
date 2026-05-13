# Regular IP Stack vs 6LoWPAN Stack

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

## Links

[[Edge Computing & IoT]]
