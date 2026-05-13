# HTTP GET

`GET` requests a representation of a resource.

Example:

```http
GET /parts HTTP/1.1
Host: www.parts-depot.com
```

`GET` should be **safe**, meaning it should not change server state.

It should also be **idempotent**, meaning repeating the same request has the same intended effect as sending it once.


Example use in IoT:

```http
GET /rooms/1/temperature HTTP/1.1
Host: edge.local
```

This could return the current temperature measurement.

---

## Links

[[Edge Computing & IoT]]