# Why TCP/HTTP Is Heavy for IoT

Traditional HTTP over TCP and TLS requires several message exchanges before the actual request is sent.

A simplified setup may include:

1. TCP SYN
2. TCP SYN + ACK
3. TCP ACK
4. TLS handshake messages
5. HTTP request
6. HTTP response

For constrained devices, this can be expensive in bytes, time, and energy.

That is why IoT systems often prefer:

$$\Large
\text{CoAP} + \text{UDP} + \text{6LoWPAN}
$$

instead of full HTTP/TCP when devices and networks are highly constrained.

---

## Links

[[Edge Computing & IoT]]