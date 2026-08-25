---
layout: single 
classes: wide
title: "ESP32 Flood Sensor Unit"
excerpt: "A field-deployable IoT sensor module for collecting real-time water-level data for eLikas."
header:
  teaser: /assets/images/esp32-teaser.jpg
author_profile: true
---

As part of eLikas, I developed an **IoT sensor module** to collect **real-time water-level measurements** and integrate physical flood data directly into the platform's mapping system.

Before building the prototype, I established several design principles based on how the sensor would eventually be used in the field. It needed to be:

1. **Modular and cost-effective** — Components should be readily available and replaceable, allowing individual parts to be upgraded or swapped without redesigning the entire system.
2. **Field-ready** — The unit needed to remain operational when deployed in locations where regular physical access would be difficult.
3. **Reliable and independent** — The sensor needed to collect, timestamp, and transmit measurements with minimal human intervention.
4. **Replicable** — The design should be practical to reproduce across multiple deployment sites without relying on specialized, proprietary, or difficult-to-source components.


### Building the Hardware

I assembled the prototype from readily available components, combining two 18650 cells for the power source, a charging and battery-management circuit, a physical on-off rocker switch, a push button for interfacing with the firmware, and I2C LCD for status feedback. The ESP32 (with a Wi-Fi capable chip), power circuitry, and display were wired together with the ultrasonic sensor to form a single self-contained unit.

For the enclosure, I repurposed a **weatherproof outdoor junction box** with a transparent cover rather than fabricating a custom housing. I used a mini hand drill to cut and fit the openings for the sensor, controls, and other interfaces, allowing the electronics to remain protected while keeping the important physical components accessible.

The hardware design was paired with **over-the-air (OTA) firmware updates through
GitHub Releases**. This allows deployed units to receive firmware improvements
remotely, reducing the need to physically access each sensor when fixing bugs or
adding functionality.


### From Measurement to Data

The firmware measures the distance between the ultrasonic sensor and the water surface, then applies **signal filtering** and **adaptive sampling** to reduce unreliable readings (more details about the measurement algorithm on Github). I also implemented **NTP time synchronization** since measurements needed to be associated with an accurate timestamp for monitoring.

Rather than hardcoding network credentials, I built **Wi-Fi provisioning** into the firmware. This allows the sensor to be configured for the network where it is deployed without modifying and reflashing the firmware.


### Sensor → API → eLikas

Once a reading is collected, the ESP32 packages the measurement as **JSON** and sends it to the eLikas HTTP API along with the sensor identifier, timestamp, and authentication data.

```json
{
  "apiKey": "A_SECURE_KEY",
  "sensorCode": "SR-XXXXXX",
  "waterLevel": 1.45,
  "sensorTimestamp": "2026-04-11 14:27:21"
}
```

The API receives the payload, processes the measurement, and surfaces it on the platform, allowing it to become another source of real-time information on the eLikas map alongside crowdsourced reports.