# Lecture 9 and 10 Edge IoT Wiki Cells

These notes convert the lecture subjects into copyable wiki-style Markdown cells. Inline math uses `$...$`, and larger equations use `$$\Large ...$$`.

---

# Lecture 9 — CoAP

```md
# CoAP — REST for Constrained Devices

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
```

---

```md
# Why CoAP Exists

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
```

---

```md
# What CoAP Is and Is Not

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
```

---

```md
# CoAP Architecture

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
```

---

```md
# CoAP Features

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
```

---

```md
# CoAP Client/Server Model

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
```

---

```md
# CoAP Message Types

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
```

---

```md
# CoAP Message Header

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
```

---

```md
# CoAP Tokens

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
```

---

```md
# Piggybacked Response in CoAP

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
```

---

```md
# Separate Response in CoAP

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
```

---

```md
# Dealing with Packet Loss in CoAP

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
```

---

```md
# CoAP Options

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
```

---

```md
# CoAP Caching

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
```

---

```md
# CoAP Proxying

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
```

---

```md
# CoAP Observation

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
```

---

```md
# CoAP Block Transfer

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
```

---

```md
# CoAP Resource Discovery

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
```

---

```md
# CoRE Link Format

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
```

---

```md
# Resource Directory in CoAP

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
```

---

```md
# CoRE Link Format Semantics

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
```

---

```md
# CoRE Interfaces

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
```

---

```md
# CoAP Security

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
```

---

```md
# Tiny CoAP Sensors

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
```

---

```md
# CoAP Summary

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
```

---

# Lecture 10 — MQTT

```md
# MQTT — Lightweight Publish/Subscribe Messaging

MQTT is a lightweight messaging protocol designed for IoT and machine-to-machine communication.

MQTT stands historically for **MQ Telemetry Transport**, although the acronym is no longer treated as having that exact meaning.

The key idea of MQTT is:

> Devices do not send messages directly to each other. Instead, they communicate through a broker.

MQTT uses a **publish/subscribe** model.

There are three main roles:

| Role | Meaning |
|---|---|
| Publisher | Sends messages |
| Subscriber | Receives messages |
| Broker | Central server that routes messages |

Example:

```text
Temperature sensor → publishes "25°C" → MQTT Broker
MQTT Broker → forwards message → subscribed clients
```

MQTT usually runs over TCP/IP and uses TCP port `1883` by default.

It is designed to be:

- lightweight
- bandwidth efficient
- simple to implement
- suitable for unreliable networks
- useful for IoT and M2M systems
```

---

```md
# MQTT Publish/Subscribe Model

MQTT uses a publish/subscribe model.

Instead of one device directly sending data to another device, devices communicate through a broker.

Example:

```text
Publisher → MQTT Broker → Subscriber
```

A publisher sends a message to a **topic**.

Example:

```text
Topic: home/kitchen/temperature
Payload: 23.5
```

A subscriber subscribes to a topic.

Example:

```text
Subscribe: home/kitchen/temperature
```

When the publisher sends a new message, the broker forwards it to all subscribers of that topic.

The publisher does not need to know who receives the message.

The subscriber does not need to know who produced the message.

This creates loose coupling:

$$\Large
\text{Publisher} \not\leftrightarrow \text{Subscriber}
$$

Both only need to know the broker and the topic.
```

---

```md
# MQTT Broker

The MQTT broker is the central server in MQTT communication.

It receives published messages and forwards them to subscribers.

Example:

```text
Sensor → Broker → Dashboard
Sensor → Broker → Database
Sensor → Broker → Alert System
```

The broker is responsible for:

- accepting client connections
- receiving published messages
- managing subscriptions
- forwarding messages to matching subscribers
- handling quality of service
- storing retained messages if configured
- managing persistent sessions if configured

Without the broker, MQTT clients do not normally communicate directly.

A simple mental model is:

$$\Large
\text{Broker} = \text{message router}
$$

Popular MQTT broker implementations include Mosquitto, HiveMQ, and ActiveMQ.
```

---

```md
# MQTT Clients

In MQTT, both publishers and subscribers are clients.

A client can be:

- only a publisher
- only a subscriber
- both publisher and subscriber

Example:

```text
Temperature sensor:
- publishes temperature values

Mobile app:
- subscribes to temperature values
- publishes control commands

Smart light:
- subscribes to control commands
- publishes status updates
```

A device can therefore both send and receive information.

Example:

```text
Smart light subscribes to:
home/livingroom/light/set

Smart light publishes to:
home/livingroom/light/status
```

This makes MQTT flexible for IoT systems where many devices communicate indirectly through a broker.
```

---

```md
# MQTT Decoupling

The publish/subscribe model decouples communication in three important ways.

## 1. Space Decoupling

Publishers and subscribers do not need to know each other's IP addresses or ports.

They only need to know the broker.

```text
Publisher → Broker
Subscriber → Broker
```

## 2. Time Decoupling

Publisher and subscriber do not necessarily need to be active at the exact same time, especially when persistent sessions or retained messages are used.

## 3. Synchronization Decoupling

The subscriber does not need to block and wait while the publisher is producing data.

The broker handles message routing.

The key idea is:

$$\Large
\text{Publishers and subscribers are independent}
$$

This is useful in IoT because devices may sleep, disconnect, reconnect, or operate at different times.
```

---

```md
# MQTT Topics

MQTT routes messages using **topics**.

A topic is a UTF-8 string that names a category of messages.

Example:

```text
home/kitchen/temperature
```

Topics are usually hierarchical, using `/` as a separator.

Example:

```text
mycar/wheels/left/front/temperature
```

This can be read as:

```text
mycar
 └── wheels
     └── left
         └── front
             └── temperature
```

Good MQTT topic names should usually:

- use printable ASCII characters
- avoid whitespace
- avoid a leading `/`
- be structured hierarchically
- describe the resource clearly

Example topic structure for a smart home:

```text
home/livingroom/temperature
home/livingroom/humidity
home/kitchen/temperature
home/bedroom/light/status
home/bedroom/light/set
```

Topics are central to MQTT because subscribers choose what messages they receive based on topic filters.
```

---

```md
# MQTT Topic Wildcards

MQTT supports wildcards for subscribing to multiple topics.

There are two main wildcards:

| Wildcard | Meaning |
|---|---|
| `+` | Single-level wildcard |
| `#` | Multi-level wildcard |

## Single-Level Wildcard: `+`

The `+` wildcard matches exactly one topic level.

Example:

```text
mycar/wheels/+/+/temperature
```

This matches:

```text
mycar/wheels/left/front/temperature
mycar/wheels/right/back/temperature
```

But it does not match:

```text
mycar/wheels/temperature
```

because that has fewer levels.

## Multi-Level Wildcard: `#`

The `#` wildcard matches multiple levels and must be at the end of the topic filter.

Example:

```text
mycar/#
```

This matches:

```text
mycar/speed
mycar/wheels/left/front/temperature
mycar/engine/status
```

Wildcards are useful when a subscriber wants a group of related messages.
```

---

```md
# MQTT Reserved Topics

MQTT topics that start with `$` are reserved for broker-internal information.

A common reserved topic prefix is:

```text
$SYS/
```

Examples:

```text
$SYS/broker/clients/connected
$SYS/broker/messages/sent
$SYS/broker/uptime
```

These topics can provide information about the broker itself, such as:

- number of connected clients
- number of sent messages
- broker uptime
- load or statistics

Normal application topics should not start with `$`.

For example, use:

```text
home/kitchen/temperature
```

instead of:

```text
$home/kitchen/temperature
```

The `$` namespace is for broker statistics and internal broker information.
```

---

```md
# MQTT Connection

An MQTT client must first connect to the broker.

The basic connection flow is:

```text
Client → CONNECT → Broker
Client ← CONNACK ← Broker
```

After connecting, the client can publish messages, subscribe to topics, or unsubscribe from topics.

MQTT also uses keep-alive messages to check that the connection is still active:

```text
Client → PINGREQ → Broker
Client ← PINGRESP ← Broker
```

When the client wants to close the connection cleanly, it sends:

```text
Client → DISCONNECT → Broker
```

The simplified lifecycle is:

$$\Large
\text{CONNECT} \rightarrow \text{CONNACK} \rightarrow \text{MQTT traffic} \rightarrow \text{DISCONNECT}
$$

This connection is built on top of TCP.
```

---

```md
# MQTT Subscribe and Unsubscribe

A client subscribes to topics to receive messages.

Example:

```text
Client → SUBSCRIBE home/kitchen/temperature
Broker → SUBACK
```

After this, the broker forwards matching messages to the client.

A client can subscribe to multiple topics:

```text
SUBSCRIBE
- home/kitchen/temperature
- home/livingroom/humidity
- home/bedroom/light/status
```

A client can also unsubscribe:

```text
Client → UNSUBSCRIBE home/kitchen/temperature
Broker → UNSUBACK
```

Important detail:

> MQTT clients do not need to create a topic before publishing or subscribing to it.

Topics are used dynamically. If a client publishes to a topic, the broker can route that message to any matching subscribers.
```

---

```md
# MQTT Publishing

Publishing means sending a message to a topic.

A published MQTT message contains:

- topic
- payload
- quality of service level

Example:

```text
PUBLISH
Topic: home/kitchen/temperature
Payload: 24.1
QoS: 1
```

The broker receives the message and forwards it to subscribers whose topic filters match.

Example:

```text
Publisher → Broker:
home/kitchen/temperature = 24.1

Broker → Subscriber 1:
home/kitchen/temperature = 24.1

Broker → Subscriber 2:
home/kitchen/temperature = 24.1
```

The publisher does not need to know how many subscribers exist.

The core idea is:

$$\Large
\text{Publisher sends once} \rightarrow \text{Broker distributes}
$$
```

---

```md
# MQTT Payloads

MQTT is data agnostic.

This means MQTT does not care what format the payload uses.

The payload can be:

- plain text
- binary data
- JSON
- XML
- sensor values
- encoded messages

Examples:

```text
Payload: 25.3
```

```json
{
  "temperature": 25.3,
  "unit": "C"
}
```

```text
Payload: binary firmware data
```

MQTT only transports the payload. The application must decide how to interpret it.

This is different from protocols that strongly define the structure of application data.

The advantage is flexibility.

The disadvantage is that publishers and subscribers must agree on the payload format.
```

---

```md
# MQTT Quality of Service

MQTT provides three Quality of Service levels.

| QoS | Meaning | Description |
|---|---|---|
| `0` | At most once | Fire and forget |
| `1` | At least once | Message arrives, but duplicates may happen |
| `2` | Exactly once | Message arrives exactly once |

There is a tradeoff:

$$\Large
\text{Higher QoS} \Rightarrow \text{more reliability but more overhead}
$$

$$\Large
\text{Lower QoS} \Rightarrow \text{less overhead but less reliability}
$$

QoS 0 is fastest but least reliable.

QoS 2 is most reliable but slowest and most expensive.

For many sensor readings, QoS 0 or QoS 1 is enough.

For important commands, QoS 1 or QoS 2 may be better.
```

---

```md
# MQTT QoS 0 — At Most Once

QoS 0 means:

> The message is delivered at most once.

It is also called **fire and forget**.

The publisher sends the message once, and no acknowledgement is required.

Example:

```text
Publisher → PUBLISH QoS=0 → Broker
```

There is no guarantee that the message arrives.

QoS 0 is useful when:

- messages are frequent
- occasional loss is acceptable
- low overhead matters more than reliability

Example:

```text
home/sensor/temperature = 22.3
```

If one temperature reading is lost, the next one may arrive soon anyway.

QoS 0 is commonly used for periodic sensor data where every single reading is not critical.
```

---

```md
# MQTT QoS 1 — At Least Once

QoS 1 means:

> The message is delivered at least once.

The publisher sends the message and waits for an acknowledgement.

Flow:

```text
Publisher → PUBLISH QoS=1 → Broker
Publisher ← PUBACK ← Broker
```

If the publisher does not receive `PUBACK`, it may retransmit the message.

This means duplicates are possible.

Example:

```text
Message: open_window_detected
```

The subscriber might receive it twice.

Therefore, applications using QoS 1 should be able to handle duplicate messages.

QoS 1 is useful when delivery is important, but duplicate handling is acceptable.
```

---

```md
# MQTT QoS 2 — Exactly Once

QoS 2 means:

> The message is delivered exactly once.

It uses a four-step handshake.

Flow:

```text
Publisher → PUBLISH QoS=2 → Broker
Publisher ← PUBREC ← Broker
Publisher → PUBREL → Broker
Publisher ← PUBCOMP ← Broker
```

This gives the strongest delivery guarantee, but it has the highest overhead.

QoS 2 is useful when duplicate messages would be harmful.

Example:

```text
charge_customer_account
unlock_door_command
execute_payment
```

For many IoT sensor applications, QoS 2 may be unnecessary because it costs more bandwidth, memory, and processing.

A simple rule:

```text
QoS 0 → fastest
QoS 1 → reliable enough for many cases
QoS 2 → strongest guarantee, highest overhead
```
```

---

```md
# MQTT QoS Has Two Delivery Parts

MQTT QoS must be understood in two separate parts:

1. Publisher to broker
2. Broker to subscriber

The publisher sets a QoS level when publishing a message:

```text
Publisher → Broker
PUBLISH topic, payload, QoS=1
```

The subscriber also has a QoS level in its subscription:

```text
Subscriber → Broker
SUBSCRIBE topic, QoS=2
```

The actual delivery from broker to subscriber depends on the subscription and broker behavior.

This means the message path is not just one QoS decision.

It is better to think of it as:

$$\Large
\text{Publisher QoS} + \text{Subscription QoS} = \text{end-to-end delivery behavior}
$$

For example, a publisher may send with QoS 1, while a subscriber receives with QoS 0 depending on its subscription.
```

---

```md
# MQTT Retained Messages

A retained message is the last stored message for a topic.

When a new subscriber subscribes to that topic, the broker immediately sends the retained message.

Example:

```text
Topic: home/livingroom/light/status
Retained payload: off
```

A new subscriber connects and subscribes:

```text
SUBSCRIBE home/livingroom/light/status
```

The broker immediately sends:

```text
off
```

This is useful because the subscriber does not need to wait for the next update.

Retained messages are good for state-like information:

- current temperature
- current light status
- device availability
- last known battery level

They are less suitable for event-like information where old messages should not be replayed.

Example of state:

```text
light/status = on
```

Example of event:

```text
button/pressed
```
```

---

```md
# MQTT Persistent Sessions

MQTT can use persistent sessions for clients with unstable network connectivity.

A persistent session lets the broker remember information about a client, such as:

- subscriptions
- undelivered messages
- session state

This is useful when a device disconnects and later reconnects.

Example:

```text
Sensor dashboard disconnects
Broker keeps subscription
Dashboard reconnects
Broker resumes delivery
```

Persistent sessions are important for IoT because many devices:

- sleep to save energy
- lose wireless connectivity
- move between networks
- reconnect frequently

The core idea is:

$$\Large
\text{Temporary disconnect} \neq \text{lost session}
$$

Persistent sessions improve reliability for unstable clients.
```

---

```md
# MQTT Last Will and Testament

MQTT supports a feature called **Last Will and Testament**.

A client can tell the broker in advance:

> If I disconnect unexpectedly, publish this message for me.

Example:

```text
Client: sensor-1
Will topic: devices/sensor-1/status
Will payload: offline
```

If the client disconnects unexpectedly, the broker publishes:

```text
devices/sensor-1/status = offline
```

This is useful for detecting failures.

Example use cases:

- sensor goes offline
- robot disconnects
- gateway loses power
- device crashes

A normal clean disconnect does not trigger the will message.

The will message is only used when the broker detects an unexpected connection loss.
```

---

```md
# MQTT Session Awareness

MQTT is session aware.

This means it can keep track of client state across communication.

Depending on configuration, the broker may remember:

- client ID
- subscriptions
- pending messages
- retained state
- last will information

This is useful for IoT systems where devices are not always online.

Example:

```text
Battery-powered sensor sleeps
Sensor wakes up
Sensor reconnects
Broker recognizes the session
```

Session awareness helps MQTT support unreliable networks and intermittent connectivity.

The main advantage is that devices do not always need to rebuild their full communication state from scratch.
```

---

```md
# MQTT vs CoAP

MQTT and CoAP are both designed for IoT, but they follow different communication models.

| Feature | MQTT | CoAP |
|---|---|---|
| Main model | Publish/subscribe | Request/response |
| Transport | TCP | Usually UDP |
| Central component | Broker | No broker required |
| Communication style | Topic-based messaging | REST-style resources |
| Good for | Event streams and telemetry | Resource access and REST APIs |
| Reliability | Provided through TCP and MQTT QoS | Provided through confirmable messages |
| Discovery | Topic conventions or external systems | Built-in resource discovery |

MQTT example:

```text
Sensor publishes to:
home/kitchen/temperature
```

CoAP example:

```text
Client requests:
GET /temperature
```

A simple distinction:

$$\Large
\text{MQTT} = \text{message distribution through broker}
$$

$$\Large
\text{CoAP} = \text{REST-style access to resources}
$$

Use MQTT when many clients need to receive event streams.

Use CoAP when clients need to read or modify resources on constrained devices.
```

---

```md
# MQTT Efficiency

MQTT is designed to be lightweight compared with HTTP.

It has:

- small packet overhead
- binary encoding
- simple message types
- efficient publish/subscribe routing
- support for low-bandwidth networks

However, MQTT runs over TCP, which means it has TCP connection overhead.

This can be good or bad depending on the scenario.

Advantages of TCP:

- reliable byte stream
- ordered delivery
- congestion control

Disadvantages of TCP:

- connection setup overhead
- memory cost
- possible inefficiency on lossy wireless networks

MQTT is often efficient for long-lived connections where many messages are sent over time.

Example:

```text
Sensor connects once
Sensor publishes every 10 seconds
Connection stays open
```

This avoids repeatedly setting up new connections.
```

---

```md
# MQTT and Packet Loss

MQTT runs over TCP, so packet loss is handled by TCP retransmission.

This gives reliable transport, but it can also create performance issues on lossy links.

When packet loss occurs, TCP may:

- retransmit lost packets
- reduce sending rate
- increase latency
- delay later data because of ordered delivery

MQTT also has its own QoS levels above TCP.

This means reliability can exist at multiple layers:

```text
MQTT QoS
TCP reliability
IP networking
Link-layer retransmissions
```

In constrained wireless networks, too much reliability at multiple layers can add overhead.

The design question is:

$$\Large
\text{How much reliability do we need, and at which layer?}
$$

For frequent sensor data, lower QoS may be enough.

For important control messages, higher QoS may be justified.
```

---

```md
# MQTT Use Cases

MQTT is well suited for IoT scenarios where devices send small messages to many consumers.

Common use cases include:

- telemetry
- sensor monitoring
- smart home systems
- vehicle data
- industrial monitoring
- device status updates
- alerts and notifications

Example smart home topics:

```text
home/livingroom/temperature
home/livingroom/humidity
home/kitchen/motion
home/bedroom/light/status
home/bedroom/light/set
```

Example industrial topics:

```text
factory/line1/motor3/temperature
factory/line1/motor3/vibration
factory/line1/motor3/status
```

MQTT works especially well when:

- devices publish small updates
- many subscribers need the same data
- clients may connect and disconnect
- low bandwidth matters
- a broker-based architecture is acceptable
```

---

```md
# MQTT Summary

MQTT is a lightweight publish/subscribe messaging protocol for IoT and machine-to-machine communication.

Important concepts:

- MQTT uses a broker.
- Clients can publish and subscribe.
- Messages are routed by topics.
- Topics are hierarchical strings.
- Wildcards allow flexible subscriptions.
- MQTT usually runs over TCP.
- Default port is `1883`.
- MQTT supports three QoS levels.
- QoS 0 means at most once.
- QoS 1 means at least once.
- QoS 2 means exactly once.
- Retained messages store the latest state for a topic.
- Persistent sessions help clients with unstable connectivity.
- Last Will and Testament helps detect unexpected disconnects.

A simple mental model is:

$$\Large
\text{MQTT} = \text{lightweight topic-based messaging through a broker}
$$

MQTT is best when IoT devices need to publish data streams or events to multiple consumers.
```