# Home-Automation / Greenhouse Hardware Candidates — Prep Only

**Status:** preparation-only purchasing/research note  
**Snapshot date:** 2026-10-24  
**Do not propagate automatically into Research, Implementation Harness Setup, Implementation, or Architecture Review requirements.**

This file is a shortlist of inexpensive physical devices that could materially improve Home Assistant / Greenhouse-Agent experiments while remaining useful afterwards.

Nothing here is an approved purchase requirement.

Availability and prices should be rechecked before buying.

---

## Selection goals

Prioritize devices that:

- are inexpensive;
- have good Home Assistant / Zigbee2MQTT / ESPHome integration paths;
- exercise different useful capabilities (sensor, actuator, power, water, contact, mesh);
- remain useful after the experiment;
- avoid proprietary hubs where practical;
- can work with the planned real HAOS VM.

A mixed protocol set is useful because the system should not only work with one ecosystem.

---

# Priority A — best initial value

## 1. Zigbee coordinator

### Budget choice: SONOFF ZBDongle-E or ZBDongle-P

Observed current SONOFF Germany pricing for Zigbee USB Dongle Plus family: about **€24.90**.

Home Assistant ZHA currently documents both SONOFF ZBDongle-E and ZBDongle-P as compatible adapters.

Why useful:

- enables real Zigbee device integration against the HAOS VM;
- supports many cheap battery sensors;
- exercises coordinator/device pairing and availability behavior;
- remains useful in a permanent Home Assistant setup;
- mains-powered Zigbee devices can later act as mesh routers.

Implementation note:

- pass the USB coordinator through to the HAOS VM;
- use either ZHA or Zigbee2MQTT according to the experiment;
- do not attach one Zigbee device to multiple coordinators simultaneously.

### Alternative: Home Assistant Connect ZBT-2

Official Home Assistant recommendation for new ZHA networks.

Observed MSRP: **€45**; German retail observed around **€50–51**.

Advantages:

- official Home Assistant hardware/firmware path;
- Zigbee or Thread;
- simplest supported ZHA experience.

Why not first budget pick:

- roughly twice the price of the SONOFF dongle for the current experiments.

Suggested approach:

**Buy ZBT-2 only if the additional official-support/Thread value matters enough at purchase time; otherwise start with a compatible SONOFF USB coordinator.**

Sources:
- https://www.home-assistant.io/integrations/zha/
- https://www.home-assistant.io/connect/zbt-2/
- https://sonoff.tech/en-de/collections/gateway-sensors

---

## 2. Greenhouse air temperature/humidity

### SONOFF SNZB-02WD

Observed price: **€19.90**

Relevant characteristics:

- Zigbee 3.0;
- IP65 enclosure;
- temperature + humidity;
- ±0.2 °C temperature accuracy stated by manufacturer;
- ±2 % RH humidity accuracy stated by manufacturer;
- CR2477 battery;
- LCD display.

Why it is a strong first Greenhouse-Agent sensor:

- suitable for humid/splash-prone environments;
- directly measures two of the most important greenhouse variables;
- useful afterwards in bathroom, basement, storage area, etc.;
- tests real sleepy/battery-powered Zigbee sensor behavior.

Note:

IP65 does not mean submersible or suitable for high-pressure water.

Sources:
- https://sonoff.tech/de-de/products/snzb-02wd-ip65-zigbee-lcd-smart-temperature-humidity-sensor
- https://support.sonoff.tech/snzb-02wd-usermanual/

---

## 3. General-purpose switched load + power telemetry

### Shelly Plug M Gen3

Observed price: **€12.90**

Relevant characteristics:

- Wi-Fi + Bluetooth;
- Matter-compatible;
- real-time power monitoring;
- appliance switching;
- up to 13 A / 3000 W resistive load according to Shelly;
- overheating protection.

Why useful:

- can switch a fan, lamp, small pump or other experimental load;
- gives actual power telemetry to the agent;
- exercises a non-Zigbee path alongside Zigbee;
- remains broadly useful around the house afterwards.

Safety:

Use only within rated load/device conditions. For pumps/heaters/inductive loads, confirm the actual load characteristics and the manufacturer's suitability before switching.

Sources:
- https://www.shelly.com/de
- https://www.shelly.com/blogs/documentation/whats-the-difference-between-the-plug-s-plug-m-and-plug-pm-gen3

---

# Priority B — very useful after the basic loop works

## 4. Water/leak detection

### SONOFF SNZB-05P

Observed SONOFF price: about **€19.90**

Exposes through Zigbee2MQTT:

- water leak state;
- battery state;
- low-battery state.

Why useful:

- meaningful physical-safety/failure input;
- directly useful near irrigation/reservoir/pumps;
- reusable under sink, washing machine, dishwasher, etc.;
- good test for safety-triggered automation.

Sources:
- https://www.zigbee2mqtt.io/devices/SNZB-05P
- https://sonoff.tech/en-de/collections/gateway-sensors

---

## 5. Door/window/contact state

### SONOFF SNZB-04P

Observed SONOFF price: about **€15.90**

Why useful:

- greenhouse/window/door state;
- tests event-driven binary sensors;
- can be repurposed for ordinary doors/windows afterwards;
- useful input for ventilation/safety logic.

Source:
- https://sonoff.tech/en-de/collections/gateway-sensors

---

## 6. Cheap ESPHome experimental node

### Seeed Studio XIAO ESP32-C3

Observed BerryBase price: **from €7.90**

Why useful:

- Wi-Fi + BLE;
- cheap programmable sensor node;
- excellent platform for custom ESPHome sensors;
- reusable far beyond this experiment.

### Capacitive soil moisture sensor

Two inexpensive observed options:

- BerryBase generic analog capacitive sensor: **€2.60**
- Seeed Grove corrosion-resistant capacitive soil sensor: **€6.90**

Why useful:

- lets us test soil moisture without committing to one proprietary Zigbee device;
- calibration and sensor drift become explicit experimental concerns;
- ESPHome can expose the result to Home Assistant.

### BH1750 light sensor

Observed BerryBase price: **€2.40**

Why useful:

- greenhouse illumination input;
- cheap I²C sensor;
- reusable for many embedded projects.

Combined value:

One ESP32-C3 can potentially host several simple sensors, making this a very cheap custom Greenhouse-Agent fixture.

Important:

These modules need wiring/enclosure/power and must be protected appropriately from humidity/water. Raw hobby PCBs are not greenhouse-weatherproof simply because the sensor measurement is relevant to a greenhouse.

Sources:
- https://www.berrybase.de/seeed
- https://www.berrybase.de/analoger-kapazitiver-bodenfeuchtesensor
- https://www.berrybase.de/bh1750-digitaler-lichtsensor
- https://esphome.io/components/sensor/sht4x/

---

# Priority C — buy only if/when the experiment needs it

## 7. Irrigation actuator

### SONOFF Zigbee Smart Water Valve

Observed price: **€29.90**

Manufacturer positioning:

- Zigbee 3.0;
- installs between water tap and hose;
- irrigation schedules;
- intended for lawns/gardens/beds;
- supports open-source home-automation integration via compatible SONOFF Zigbee dongles.

Why useful:

- actual physical actuator for Greenhouse-Agent watering;
- much more representative than toggling a dummy relay;
- can remain useful for real irrigation afterwards.

Why not Priority A:

- requires an actual suitable water/hose setup;
- physical-water failure modes increase the stakes;
- should come after sensing/safety/control logic is already behaving sensibly.

Source:
- https://sonoff.tech/de-de/products/sonoff-zigbee-smart-water-valve

---

## 8. Off-the-shelf Zigbee soil sensor

Zigbee2MQTT currently supports several inexpensive soil-sensor families, including variants of:

- Tuya TS0601 soil sensors;
- COOLO CS-201Z;
- HOBEIAN ZG-303Z;
- Haozee HZ-SL10;
- GIEX GX06;
- several soil-fertility multi-sensors.

Potentially exposed values include:

- soil moisture;
- soil temperature;
- sometimes humidity/illuminance/fertility;
- battery state.

Why this is not an immediate recommendation:

The low-cost Tuya/generic market contains many visually similar hardware variants and manufacturer fingerprints.

**Do not buy a generic "TS0601 soil sensor" solely from the marketing name.**

Before purchase, verify the exact model/manufacturer fingerprint against Zigbee2MQTT/ZHA support and current user reports.

Sources:
- https://www.zigbee2mqtt.io/devices/TS0601_soil.html
- https://www.zigbee2mqtt.io/devices/CS-201Z.html
- https://www.zigbee2mqtt.io/devices/ZG-303Z.html
- https://www.zigbee2mqtt.io/devices/HZ-SL10.html
- https://www.zigbee2mqtt.io/devices/GX06.html

---

## 9. Motion/presence sensor

### SONOFF SNZB-03P

Observed price: **€16.51**

Why useful:

- not essential to the Greenhouse-Agent MVP;
- cheap event-driven occupancy/movement input;
- highly reusable later for home automation;
- useful for testing local automations and event latency.

Source:
- https://sonoff.tech/de-de/products/sonoff-zigbee-motion-sensor-snzb-03p

---

# Suggested minimal purchase order

If spending must stay low, prioritize in this order:

1. **Zigbee coordinator** — only if none is already available;
2. **SNZB-02WD** — real greenhouse air sensing;
3. **Shelly Plug M Gen3** — physical actuator + power telemetry + non-Zigbee protocol;
4. **SNZB-05P** — water-safety signal;
5. **XIAO ESP32-C3 + soil sensor + BH1750** — cheap custom ESPHome experimentation;
6. **SNZB-04P** — contact sensor;
7. **SONOFF water valve** — only once water-control logic is ready for real physical testing;
8. other soil/presence/multi-sensors as experiments justify them.

This sequence intentionally gives useful sensor + actuator + failure-state coverage before buying specialized gadgets.

---

# Research notes

## Zigbee network

Home Assistant ZHA currently recommends Home Assistant Connect ZBT-2 for a new network but also documents SONOFF ZBDongle-E/P as known compatible adapters.

One Zigbee network has one coordinator.

Mains-powered Zigbee devices commonly act as routers; battery-powered sensors are normally end devices.

## ZHA vs Zigbee2MQTT

Both are reasonable experiment targets.

Do not decide permanently in this preparation shopping note.

The Research/Implementation work should choose based on the actual architecture/evaluation need.

## ESPHome

ESPHome is particularly attractive for custom greenhouse sensing because inexpensive ESP32 hardware can expose custom sensors cleanly to Home Assistant.

It also gives the experiments a second integration style beyond commercial Zigbee products.

---

# Purchase-status rule

Nothing in this file is assumed to be physically available to Implementation until the owner explicitly says it was purchased/received and adds it to the implementation input/inventory.

Do not copy this shopping shortlist into the future-facing requirements documents merely because it exists.
