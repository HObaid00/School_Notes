# Internet Architecture: Network vs Stack Connections

Two hosts may be connected through routers at the network level, but each protocol layer behaves as if it communicates with the matching layer on the other host.

For example:

- The application layer sends HTTP messages to the remote application.
- The transport layer sends TCP or UDP data to the remote transport layer.
- The IP layer routes packets through intermediate routers.
- The link layer only handles local next-hop communication.

Routers usually inspect and forward IP packets, but they do not process the application-layer content in normal forwarding.

---

## Links

[[Edge Computing & IoT]]