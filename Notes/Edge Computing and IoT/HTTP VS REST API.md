# HTTP VS REST API 

REST is a resource-oriented way to design APIs.

The core pattern is:

$$\Large
\text{URI identifies resource} + \text{HTTP method defines operation}
$$

Examples:

```text
GET    /sensors/1/value
PUT    /actuators/1/state
POST   /events
DELETE /rules/5
```

For IoT and edge systems, REST is useful because it provides a familiar and uniform way to expose sensors, actuators, rooms, devices, events, and configuration.

When normal HTTP is too expensive, constrained REST protocols such as CoAP keep the same architectural idea with lower overhead.