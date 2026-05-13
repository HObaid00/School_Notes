# Stateless vs Stateful Header Compression

**Stateless header compression** uses information that both sides can infer without preconfigured shared context.

Example: A link-local IPv6 address may be derived from the link-layer address.

**Stateful header compression** uses shared context, such as a known network prefix. This can compress more, but the context must be distributed and maintained.

Trade-off:

| Compression type | Advantage | Disadvantage |
|---|---|---|
| Stateless | Simple, no shared setup | Less compression |
| Stateful | Better compression | Requires context management |

---

## Links

[[Edge Computing & IoT]]

