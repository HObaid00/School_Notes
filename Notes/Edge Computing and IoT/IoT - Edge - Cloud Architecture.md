# IoT - Edge - Cloud Architecture

The **IoT-edge-cloud** model divides work between three layers.

| Layer | Main role | Typical strengths | Typical limits |
|---|---|---|---|
| IoT devices | Sense and act | Close to physical world, low cost | Limited CPU, memory, power, and networking |
| Edge node | Local processing and gateway functions | Faster response, local filtering, local control | Less global information than cloud |
| Cloud | Central storage and large-scale analysis | High compute power, big data, machine learning | Higher latency, bandwidth cost, privacy concerns |

A useful design question is: **Where should each computation happen?**

For example:

- A temperature sensor should measure locally.
- A gateway may average readings and detect anomalies.
- The cloud may store historical data and train prediction models.

The design goal is not to replace the cloud. The goal is to split work intelligently.

![[Pasted image 20260511172915.png]]

---

## Links
[[Edge Computing & IoT]]