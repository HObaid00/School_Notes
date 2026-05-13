# REST API

## Representational State Transfer

**REST** is an architectural style for designing web services around resources.

The main ideas are:

- Every important entity is modeled as a resource.
- Each resource is identified by a URI.
- A uniform interface is used for all resources.
- Messages should be self-describing.
- Resources can link to other resources.

Example resource URL:

```text
/rooms/1/sensors/temperature
```

REST is not a formal protocol standard. It is a design style that usually uses standards such as HTTP, URI, JSON, and XML.

---

## REST Resources and URIs

A **resource** is something the API exposes. It can be a physical object, a measurement, a collection, or a service concept.

Examples:

```text
/rooms
/rooms/1
/rooms/1/sensors
/rooms/1/sensors/temperature
```

A good REST URI names resources, not implementation details.

Good:

```text
/rooms/1/sensors/temperature
```

Less good:

```text
/getTemperatureFromRoomOne
```

REST design encourages thinking in nouns/resources instead of remote procedure calls.

---

## REST and Databases

REST resources often map to database operations, but the client should not need to know the database implementation.

Example mapping:

| REST request | Possible database operation |
|---|---|
| `GET /book?ISBN=222` | `SELECT * FROM books WHERE isbn=222` |
| `PUT /order` | `INSERT INTO orders ...` |
| `POST /order/612` | `UPDATE orders WHERE id=612` |

The API hides the internal database and exposes stable resources.

This is called **loose coupling**: the client depends on the REST interface, not on how the server generates the response.

---

## Linked Resources in REST

REST responses can include links to related resources.

Example:

```xml
<Part>
  <Part-ID>00345</Part-ID>
  <Name>Widget-A</Name>
  <Specification href="http://www.parts-depot.com/parts/00345/specification"/>
</Part>
```

---

## Data Representation: JSON and XML

REST APIs need a way to represent resource state. Common formats are **JSON** and **XML**.

JSON example:

```json
{
  "partId": "00345",
  "name": "Widget-A",
  "unitCost": 0.10,
  "quantity": 10
}
```

JSON is usually more compact and common in modern APIs. XML is more verbose but supports schemas and document-oriented structures well.

---

## RESTful Interfaces for IoT

REST can model IoT systems as resources.

Example resource structure:

```text
/rooms
/rooms/1
/rooms/1/sensors
/rooms/1/sensors/temperature
/rooms/1/controllers/heating
```

Possible operations:

- `GET /rooms/1/sensors/temperature` reads a measurement.
- `PUT /rooms/1/controllers/heating` updates the heating target.
- `POST /rooms/1/events` submits a new event.

For constrained IoT devices, HTTP may be too heavy. The same REST ideas can be implemented with **CoAP**, which is designed for constrained environments and usually runs over UDP.

---

## Links

[[Edge Computing & IoT]]