

# Lecture 10 — MQTT

## MQTT — Lightweight Publish/Subscribe Messaging

MQTT is a lightweight messaging protocol designed for IoT and machine-to-machine communication.

MQTT stands historically for **MQ Telemetry Transport**, although the acronym is no longer treated as having that exact meaning.

The key idea of MQTT is:

> Devices do not send messages directly to each other. Instead, they communicate through a broker.

MQTT uses a **publish/subscribe** model.

There are three main roles:

| Role       | Meaning                             |
| ---------- | ----------------------------------- |
| Publisher  | Sends messages                      |
| Subscriber | Receives messages                   |
| Broker     | Central server that routes messages |

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

---
## MQTT Publish/Subscribe Model

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

---

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

---

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

---

## MQTT Decoupling

The publish/subscribe model decouples communication in three important ways.

### 1. Space Decoupling

Publishers and subscribers do not need to know each other's IP addresses or ports.

They only need to know the broker.

```text
Publisher → Broker
Subscriber → Broker
```

### 2. Time Decoupling

Publisher and subscriber do not necessarily need to be active at the exact same time, especially when persistent sessions or retained messages are used.

### 3. Synchronization Decoupling

The subscriber does not need to block and wait while the publisher is producing data.

The broker handles message routing.

The key idea is:

$$\Large
\text{Publishers and subscribers are independent}
$$

This is useful in IoT because devices may sleep, disconnect, reconnect, or operate at different times.

---

## MQTT Topics

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

---

## MQTT Topic Wildcards

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

---

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

---

## MQTT Subscribe and Unsubscribe

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

---

## MQTT Publishing

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

---

## MQTT Payloads

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

---

## MQTT Quality of Service

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

---

## MQTT QoS 0 — At Most Once

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

---

## MQTT QoS 1 — At Least Once

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

---

## MQTT QoS 2 — Exactly Once

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

---

## MQTT QoS Has Two Delivery Parts

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

---

## MQTT Retained Messages

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

---

## MQTT Persistent Sessions

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

---

## MQTT Last Will and Testament

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

---

## MQTT Session Awareness

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

---

## MQTT vs CoAP

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

---

## MQTT Efficiency

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

---

## MQTT and Packet Loss

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

---

## MQTT Use Cases

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

---

## MQTT Summary

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
