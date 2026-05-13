# HTTP 

**HTTP** means Hypertext Transfer Protocol. It transfers information between web clients and web servers.

A basic HTTP request contains:

- A request method
- A resource path
- Headers
- A blank line
- Optional content body

Example:

```http
GET /test.html HTTP/1.1
Host: in.tum.de
```

HTTP traditionally runs over TCP. It is text-based and widely used for web applications and APIs.

---

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

## HTTP POST

`POST` sends data to the server, often to create a subordinate resource or submit an operation.

Example:

```http
POST /orders HTTP/1.1
Host: www.parts-depot.com
Content-Type: application/json

{"part":"00345", "quantity":10}
```

`POST` is usually not safe and not idempotent. Sending the same `POST` twice may create two orders.

Example use in IoT:

```http
POST /rooms/1/events HTTP/1.1
Content-Type: application/json

{"type":"motion", "value":true}
```

---

## HTTP PUT and DELETE

`PUT` updates or replaces a resource at a known URI.

Example:

```http
PUT /rooms/1/target-temperature HTTP/1.1
Content-Type: application/json

{"value":21.5}
```

`PUT` is idempotent: sending the same update multiple times should lead to the same final state.

`DELETE` removes a resource.

Example:

```http
DELETE /rooms/1/schedules/night HTTP/1.1
```

In REST, the method describes the action, while the URI identifies the resource.

----

## Safe and Idempotent HTTP Methods

Two important REST properties are **safety** and **idempotence**.

A method is **safe** if it does not intentionally change server state.

A method is **idempotent** if repeating it has the same intended effect as doing it once.

| Method | Safe? | Idempotent? | Typical meaning |
|---|---:|---:|---|
| GET | Yes | Yes | Read resource |
| HEAD | Yes | Yes | Read metadata only |
| PUT | No | Yes | Replace/update resource |
| POST | No | No | Create subordinate resource or submit data |
| DELETE | No | Yes | Delete resource |

Understanding these properties helps design APIs that behave predictably.

---

## Links

[[Edge Computing & IoT]]