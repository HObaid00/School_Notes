# 6LoWPAN Header Compression

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

## Links

[[Edge Computing & IoT]]

