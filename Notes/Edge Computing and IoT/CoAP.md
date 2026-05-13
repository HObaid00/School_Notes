# CoAP

CoAP stands for **Constrained Application Protocol**. It is a lightweight protocol designed for IoT devices that have limited CPU power, limited memory, limited energy, and often unreliable wireless links.

The basic idea is:

> CoAP gives constrained IoT devices a REST-like communication style, similar to HTTP, but with much lower overhead.

Instead of using full HTTP over TCP, CoAP usually runs over UDP. This makes it more suitable for low-power networks such as IPv6 over 6LoWPAN.

A typical IoT protocol stack looks like this:

$$\Large
\text{Application: CoAP}
\rightarrow
\text{Transport: UDP}
\rightarrow
$$
$$\Large
\rightarrow
\text{Network: IPv6 / 6LoWPAN}
\rightarrow
\text{Link: IEEE 802.15.4}

$$

CoAP is useful when a small device, such as a temperature sensor, wants to expose resources like:

```text
/temp
/light
/humidity
/battery
```

A client can then request these resources using REST-style methods such as `GET`, `POST`, `PUT`, and `DELETE`.

Example:

```text
GET coap://sensor.local/temp
```

The server might respond:

```text
22.5 C
```

CoAP is **not** meant to replace HTTP everywhere. It is specialized for constrained environments and can be proxied to and from HTTP when needed.

---

## Why CoAP Exists

Many IoT devices used to rely on dedicated networking technologies such as Bluetooth, Zigbee, or other custom protocols. These systems often required gateways to translate between the local IoT network and the wider Internet.

CoAP exists because engineers wanted IoT devices to communicate more like normal Internet devices, but without the heavy overhead of full HTTP/TCP.

The goal is:

$$\Large
\text{Small device} + \text{lightweight IP stack} + \text{REST-style protocol}
$$

CoAP is commonly used together with:

- IPv6
- 6LoWPAN
- UDP
- IEEE 802.15.4

A normal Web system might use:

```text
HTTP → TCP → IP → Ethernet
```

A constrained IoT system might use:

```text
CoAP → UDP → IPv6 with 6LoWPAN → IEEE 802.15.4
```

The advantage is that CoAP keeps the familiar REST idea while reducing packet size, memory use, and energy consumption.

---

## What CoAP Is and Is Not

CoAP is a **RESTful application-layer protocol** for constrained IoT devices.

CoAP is:

- Efficient
- REST-like
- Designed for constrained devices and networks
- Specialized for IoT
- Easy to proxy to and from HTTP

CoAP is not:

- A general replacement for HTTP
- Simply “compressed HTTP”
- A full Web browser protocol

The important idea is that CoAP keeps the REST model:

```text
Client → request → resource
Client ← response ← resource state
```

Example:

```text
Client: GET /temperature
Server: 2.05 Content "22.5 C"
```

The resource is identified by a URI, just like in HTTP:

```text
coap://example-sensor.local/temperature
```

So CoAP is best understood as:

> REST for small devices and low-power networks.

---

## CoAP Architecture

CoAP is designed to connect two worlds:

1. The normal Internet, where HTTP is common.
2. Constrained IoT environments, where CoAP is more efficient.

A typical architecture contains:

```text
HTTP Client / Server
        |
      Proxy
        |
CoAP Client / Server
```

The proxy can translate between HTTP and CoAP.

For example:

```text
HTTP GET /light
```

can be translated by a proxy into:

```text
CoAP GET /light
```

Then the CoAP server responds with the state of the resource, such as:

```text
2.05 Content "on"
```

The proxy can then translate this back into an HTTP response.

This is useful because normal Web clients can interact with constrained IoT devices without needing to know all details of the constrained network.

---

## CoAP Features

CoAP has several features that make it suitable for IoT.

Important features include:

- URI-based resources
- REST methods: `GET`, `POST`, `PUT`, `DELETE`
- Small 4-byte base header
- UDP transport
- Optional reliability
- Multicast support
- Built-in resource discovery
- Support for caching
- Proxying to and from HTTP
- Security using DTLS

The basic REST methods work similarly to HTTP:

| Method | Meaning |
|---|---|
| `GET` | Read a resource |
| `POST` | Create or submit data |
| `PUT` | Update or replace a resource |
| `DELETE` | Delete a resource |

Example:

```text
GET /temp
```

asks for the current temperature.

```text
PUT /light
Payload: on
```

updates the light resource so that the light turns on.

The key design goal is to keep the REST model while making the protocol small enough for constrained devices.

---

## CoAP Client/Server Model

CoAP uses a client/server model.

The client sends a request. The server sends a response.

Example:

```text
Client → GET /temperature → Server
Client ← 2.05 Content "22.3 C" ← Server
```

Unlike HTTP, CoAP usually runs over UDP instead of TCP. UDP is lightweight, but it does not provide built-in sessions or reliable delivery.

Therefore, CoAP adds its own simple reliability mechanisms when needed.

CoAP has three conceptual layers:

```text
REST Request / Response
CoAP Messages
UDP
```

The REST layer describes what the client wants, such as:

```text
GET /light
```

The CoAP message layer handles how this request is sent over UDP.

The UDP layer transports the packet without creating a full TCP connection.

---

## CoAP Message Types

CoAP defines several message types.

The most important are:

| Type | Meaning |
|---|---|
| `CON` | Confirmable message |
| `NON` | Non-confirmable message |
| `ACK` | Acknowledgement |
| `RST` | Reset |

A **Confirmable** message expects an acknowledgement.

Example:

```text
Client → CON GET /humidity → Server
Client ← ACK 2.05 Content "45%" ← Server
```

A **Non-confirmable** message does not require an acknowledgement.

Example:

```text
Client → NON GET /temperature → Server
```

This is faster and cheaper, but less reliable.

The difference is:

$$\Large
\text{CON} = \text{reliable but more overhead}
$$

$$\Large
\text{NON} = \text{less overhead but less reliability}
$$

Use `CON` when the message is important. Use `NON` when occasional loss is acceptable.

---

## CoAP Message Header

CoAP has a very small base header of only **4 bytes**.

The base header contains:

| Field | Meaning |
|---|---|
| `Ver` | CoAP version |
| `T` | Message type |
| `TKL` | Token length |
| `Code` | Request method or response code |
| `Message ID` | Identifier for matching messages |

A simplified CoAP header looks like this:

```text
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Ver| T |TKL| Code | Message ID |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Token, options, payload ...   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

The `Message ID` is important because UDP does not provide a connection or session. CoAP uses message IDs to match acknowledgements and detect duplicates.

Example:

```text
CON [0x7d34] GET /temp
ACK [0x7d34] 2.05 Content "22.3 C"
```

Here, both messages use the same message ID:

```text
0x7d34
```

This lets the client know that the acknowledgement belongs to its original request.

---

## CoAP Tokens

A **token** is used by CoAP to match responses to requests.

This is especially important because UDP does not provide a session concept like TCP.

Example:

```text
Client → CON GET /light Token: 0x3f
Server → ACK 2.05 Content "on" Token: 0x3f
```

The token tells the client:

> This response belongs to the request that used token `0x3f`.

Message IDs are used for message-level reliability. Tokens are used for request/response matching.

A simple distinction is:

| Concept | Purpose |
|---|---|
| Message ID | Match messages and acknowledgements |
| Token | Match requests and responses |

This matters especially when a client has multiple requests active at the same time.

---

## Piggybacked Response in CoAP

A **piggybacked response** means that the server sends the response directly inside the acknowledgement.

Example:

```text
Client → CON GET /light
Server → ACK 2.05 Content "on"
```

The `ACK` both acknowledges the request and carries the actual response data.

This is efficient because it combines two things into one message:

$$\Large
\text{Acknowledgement} + \text{Response Payload}
$$

Piggybacked responses are useful when the server can answer quickly.

Example use case:

```text
GET /temperature
```

If the sensor already has the current value, it can immediately respond:

```text
ACK 2.05 Content "22.3 C"
```

This reduces the number of packets and saves energy.

---

## Separate Response in CoAP

A **separate response** is used when the server needs more time to process the request.

First, the server acknowledges that it received the request. Later, it sends the actual response.

Example:

```text
Client → CON GET /light
Server → ACK
```

Later:

```text
Server → CON 2.05 Content "on"
Client → ACK
```

This is useful when the requested operation takes too long for an immediate piggybacked response.

For example:

```text
GET /measurement
```

If the sensor must first wake up, sample the environment, and process the result, it may not answer immediately.

The separate response pattern avoids unnecessary retransmissions while still allowing slow operations.

---

## Dealing with Packet Loss in CoAP

CoAP often runs over UDP, and UDP does not guarantee delivery.

To handle packet loss, CoAP can use **confirmable messages**.

Example:

```text
Client → CON GET /humidity → Server
```

If the message is lost, the client waits for a timeout and retransmits:

```text
Client → CON GET /humidity → Server
```

When the server receives it, it replies:

```text
Server → ACK 2.05 Content "45%" → Client
```

The basic reliability mechanism is:

$$\Large
\text{Send} \rightarrow \text{Wait for ACK} \rightarrow \text{Retransmit if timeout}
$$

This is simpler than TCP, but good enough for many IoT scenarios.

It allows CoAP to stay lightweight while still supporting reliable communication when needed.

---

## CoAP Options

CoAP uses **options** to add metadata to a message.

Options can describe things such as:

- URI path
- URI query
- content format
- max age for caching
- proxy URI
- accepted response format

Examples of common options:

| Option | Meaning |
|---|---|
| `Uri-Path` | Resource path, such as `/temp` |
| `Uri-Query` | Query parameters |
| `Content-Format` | Payload format |
| `Accept` | Desired response format |
| `Max-Age` | Cache lifetime |
| `Proxy-Uri` | URI used by a proxy |

Example:

```text
GET /sensors/temp?unit=celsius
```

This could be represented using:

```text
Uri-Path: sensors
Uri-Path: temp
Uri-Query: unit=celsius
```

CoAP options are encoded compactly to keep messages small.

---

## CoAP Caching

CoAP includes a simple caching model.

Caching means that a response can be stored and reused for a certain time instead of asking the server again.

Example:

```text
GET /light
Response: 2.05 Content "on"
Max-Age: 30
```

This means the response can be considered fresh for 30 seconds.

The main idea is:

$$\Large
\text{Cache fresh} \Rightarrow \text{reuse response}
$$

$$\Large
\text{Cache expired} \Rightarrow \text{request again}
$$

Caching is especially useful in IoT because it can reduce:

- network traffic
- energy consumption
- delay
- load on sleeping or constrained nodes

A proxy can cache responses on behalf of constrained devices. This is useful when the device sleeps most of the time to save battery.

---

## CoAP Proxying

A CoAP proxy translates between CoAP and another protocol, often HTTP.

Example architecture:

```text
HTTP Client → Proxy → CoAP Server
```

A normal HTTP client might send:

```text
HTTP GET /light
```

The proxy translates it into:

```text
CoAP GET /light
```

The CoAP server responds:

```text
2.05 Content "on"
```

The proxy translates that back into an HTTP response:

```text
200 OK "on"
```

Proxying is useful because it connects constrained IoT networks to the normal Web.

A proxy can also cache responses, which helps reduce repeated requests to small battery-powered devices.

---

## CoAP Observation

CoAP supports a publish/subscribe-like mechanism called **Observation**.

Observation lets a client subscribe to changes in a resource.

Instead of repeatedly asking:

```text
GET /temperature
GET /temperature
GET /temperature
```

the client can observe the resource:

```text
GET /temperature Observe: 0
```

Then the server sends updates when the value changes.

Example:

```text
Client → GET /light Observe: 0
Server → 2.05 Content "off"
Server → 2.05 Content "on"
Server → 2.05 Content "off"
```

This is useful for sensor readings, such as:

- temperature
- humidity
- light level
- motion detection
- battery level

Observation reduces unnecessary polling.

The idea is:

$$\Large
\text{Polling} = \text{client repeatedly asks}
$$

$$\Large
\text{Observation} = \text{server notifies on change}
$$

---

## CoAP Block Transfer

CoAP usually sends small messages, but sometimes an IoT device needs to transfer larger data.

UDP does not provide stream-based transfer like TCP, so CoAP uses **block transfer**.

The large payload is split into smaller blocks.

Example:

```text
Block 0
Block 1
Block 2
Block 3
```

A client can request each block separately:

```text
GET /firmware Block2: 0
GET /firmware Block2: 1
GET /firmware Block2: 2
```

This is useful for:

- firmware updates
- larger sensor logs
- configuration files
- images or structured documents

The core idea is:

$$\Large
\text{Large payload} \rightarrow \text{small CoAP blocks}
$$

Block transfer allows CoAP to handle larger resources without requiring TCP.

---

## CoAP Resource Discovery

Resource discovery answers the question:

> What resources does this device provide?

For example, a device might provide:

```text
/temp
/light
/battery
/humidity
```

CoAP uses a well-known URI for discovery:

```text
/.well-known/core
```

A client can send:

```text
GET /.well-known/core
```

The server may respond with a list of resources:

```text
</light>;rt="Illuminance";ct=0,
</s/temp>;rt="Temperature";ct=0,
</dev/bat>;rt="Battery";ct=0
```

This tells the client what resources exist and how to interpret them.

Important fields include:

| Field | Meaning |
|---|---|
| `rt` | Resource type |
| `if` | Interface description |
| `ct` | Content type |
| `obs` | Observable resource |

Example:

```text
</sen/temp>;obs;if="core.s";rt="ucum:Cel";ct=0
```

This describes a temperature sensor resource that can be observed.

---

## CoRE Link Format

The **CoRE Link Format** is used by CoAP for resource discovery.

It gives machines a compact way to describe resources.

Example:

```text
</dev/bat>;rt="ipso:dev-bat";ct="0",
</sen/temp>;obs;if="core.s";rt="ucum:Cel";ct="0"
```

This can be interpreted as:

| Part | Meaning |
|---|---|
| `</dev/bat>` | Resource URI |
| `rt="ipso:dev-bat"` | Resource type: device battery |
| `ct="0"` | Content type: text/plain |
| `obs` | Resource can be observed |
| `if="core.s"` | Sensor interface |

The main idea is that a client should not need hardcoded knowledge of every device.

Instead, it can ask:

```text
GET /.well-known/core
```

and learn what the device supports.

---

## Resource Directory in CoAP

A **Resource Directory** is a central place where IoT devices can register their resources.

This is useful because many IoT devices sleep to save energy and may not always be reachable.

Instead of asking every device directly, a client can ask the resource directory.

Typical process:

1. A node registers its resources.
2. The directory stores the resource descriptions.
3. A client searches the directory.
4. The client contacts the correct node or resource.

Example:

```text
Node → POST /rd
Body: </s/temp>;rt="Temperature"
```

Later:

```text
Client → GET /rd-lookup/res?rt=Temperature
```

The directory returns matching resources.

Resource directories are useful because they reduce multicast traffic, support sleeping nodes, and allow remote lookup.

---

## CoRE Link Format Semantics

CoRE resource descriptions use small semantic labels so machines can understand resources.

Important labels include:

| Label | Meaning |
|---|---|
| `rt` | Resource type |
| `if` | Interface description |
| `ct` | Content type |
| `obs` | Observable resource |

Example:

```text
</sen/temp>;obs;if="core.s";rt="ucum:Cel";ct="0"
```

Meaning:

- `</sen/temp>` is the resource path.
- `obs` means the resource can be observed.
- `if="core.s"` means it behaves like a sensor.
- `rt="ucum:Cel"` means the value is in degrees Celsius.
- `ct="0"` means the payload is text/plain.

This helps clients understand not just where a resource is, but what it means and how it should be used.

---

## CoRE Interfaces

CoRE interfaces describe how a resource can be accessed.

Examples:

| Interface | Meaning | Common Methods |
|---|---|---|
| `core.s` | Sensor | `GET` |
| `core.p` | Parameter | `GET`, `PUT` |
| `core.a` | Actuator | `GET`, `PUT`, `POST` |
| `core.ll` | Link list | `GET` |
| `core.b` | Batch | `GET`, `PUT`, `POST` |

Example:

```text
</sen/temp>;if="core.s";rt="ucum:Cel"
```

This means the resource is a sensor. A client should usually read it using:

```text
GET /sen/temp
```

Example actuator:

```text
</light>;if="core.a";rt="light"
```

This means the resource can likely be controlled:

```text
PUT /light
Payload: on
```

Interfaces help standardize how clients interact with common IoT resources.

---

## CoAP Security

CoAP commonly uses **DTLS** for security.

DTLS stands for **Datagram Transport Layer Security**. It is similar to TLS, but adapted for UDP.

Since CoAP often runs over UDP, normal TLS is not directly used in the same way as with HTTP over TCP.

CoAP security can use:

- Pre-shared keys
- Raw public keys
- Certificates

The goal is to provide:

$$\Large
\text{Confidentiality} + \text{Integrity} + \text{Authentication}
$$

Security is important because IoT devices may control real-world systems, such as:

- doors
- lights
- heating
- sensors
- industrial equipment

Without security, attackers could read data, modify commands, or impersonate devices.

---

## Tiny CoAP Sensors

Very constrained devices can send CoAP packets with minimal code if much of the packet is precomputed.

The idea is:

1. Prepare most of the IPv6, UDP, CoAP, and payload structure in advance.
2. Keep fixed fields constant, such as addresses and identifiers.
3. Insert only the changing sensor value before transmission.

Example:

```text
Precomputed packet:
IPv6 header + UDP header + CoAP header + XML/text structure

Changing part:
temperature = 22.3
```

Instead of constructing the entire packet every time, the device only updates the sensor value.

This saves:

- CPU cycles
- memory
- energy
- implementation complexity

The main optimization idea is:

$$\Large
\text{Precompute fixed fields} + \text{insert new sensor value}
$$

This is useful for extremely small, battery-powered IoT sensors.

---

## CoAP Summary

CoAP is a lightweight RESTful protocol for constrained IoT devices.

It is designed for environments where full HTTP/TCP is too expensive.

Important concepts:

- CoAP uses REST-style resources.
- CoAP usually runs over UDP.
- It supports `GET`, `POST`, `PUT`, and `DELETE`.
- It has a small 4-byte base header.
- It supports confirmable and non-confirmable messages.
- It can handle packet loss using acknowledgements and retransmissions.
- It supports caching and proxying.
- It supports observation for publish/subscribe-like updates.
- It supports block transfer for large payloads.
- It supports resource discovery through `/.well-known/core`.

A simple mental model is:

$$\Large
\text{CoAP} = \text{HTTP-like REST for constrained IoT devices}
$$

Use CoAP when small devices need efficient, REST-style communication over low-power networks.

---

## Links

[[REST API]]
[[Edge Computing & IoT]]