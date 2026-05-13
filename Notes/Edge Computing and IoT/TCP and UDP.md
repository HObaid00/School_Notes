# TCP and UDP

**TCP** provides reliable, ordered byte-stream communication. It uses connection setup, acknowledgments, re-transmissions, and flow control.

**UDP** provides lightweight datagram communication. It has less overhead but does not guarantee delivery or ordering.

| Protocol | Reliable? | Connection setup? | Typical use |
|---|---:|---:|---|
| TCP | Yes | Yes | Web, file transfer, reliable streams |
| UDP | No | No | DNS, CoAP, real-time or constrained communication |

For constrained IoT, UDP is often preferred because it has lower overhead and works well with protocols such as CoAP.

---

## Links

[[Edge Computing & IoT]]