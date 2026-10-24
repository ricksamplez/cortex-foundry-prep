# Home-Automation / Greenhouse / Hydro Hardware Candidates — Prep Only

**Status:** preparation-only purchasing/research note  
**Snapshot date:** 2026-10-24  
**Do not propagate automatically into Research, Implementation Harness Setup, Implementation, or Architecture Review requirements.**

This file is a budget-aware shortlist of physical devices and already-owned hardware that could materially improve Home Assistant / Greenhouse-Agent / Hydroponics experiments while remaining useful afterwards.

Nothing listed as a candidate is an approved purchase requirement.

Availability/prices/integration status must be rechecked before buying.

---

# Current strategy

Prefer **Wi-Fi + BLE + ESPHome first**.

Reasons:

- the owner already operates a dedicated 2.4-GHz-only IoT Wi-Fi network on a Ubiquiti UDR7;
- most normal household traffic uses 5/6 GHz, leaving the 2.4-GHz IoT network relatively quiet;
- multiple ThermoPro TP357 BLE thermo/hygrometers are already owned and already used for greenhouse work;
- a VIVOSUN GrowHub E42A is already owned;
- avoiding Zigbee initially removes the cost of both a coordinator and new Zigbee-only sensors;
- ESPHome/M5Stack/Seeed devices remain highly reusable.

Zigbee remains attractive for later scale/battery sensors, but is deliberately **deferred rather than rejected**.

---

# Already-owned high-value hardware

## ThermoPro TP357 BLE thermo/hygrometers

Status: **already owned; no purchase required**.

Home Assistant officially supports the TP357 through the ThermoPro integration.

The integration uses Bluetooth and is classified by Home Assistant as Local Push.

Recommended experiment path:

`TP357 BLE broadcasts → ESPHome Bluetooth Proxy → HAOS Bluetooth/ThermoPro integration`

This avoids needing Bluetooth passthrough directly into the HAOS VM and lets a cheap proxy be placed physically close to the greenhouse tents.

Potential uses:

- tent temperature/humidity;
- room temperature/humidity;
- cross-checking VIVOSUN telemetry;
- thermal-response experiments around window/fan actions;
- evaluating sensor disagreement/failure handling.

Sources:

- https://www.home-assistant.io/integrations/thermopro/
- https://www.home-assistant.io/integrations/bluetooth/
- https://esphome.io/components/bluetooth_proxy/

---

## VIVOSUN GrowHub E42A — old/non-Plus model

Status: **already owned; promising existing integration target**.

A current unofficial Home Assistant HACS integration (`lientry/homeassistant-vivosun-growhub`) explicitly lists the original GrowHub **E42A** as verified working.

Current exposed functions include, depending on connected VIVOSUN hardware:

- grow-light control/brightness;
- circulation-fan control;
- duct-fan control;
- fan presets/auto thresholds;
- temperature;
- humidity;
- VPD;
- grow-plan/stage/schedule information.

Important limitation:

**The current integration is not local/offline.**

It depends on:

- VIVOSUN account credentials;
- VIVOSUN cloud;
- AWS IoT;
- outbound internet access.

Therefore:

- it is excellent as an immediate real-device integration experiment;
- it should not be mistaken for proof of local/offline E42A control;
- a later local protocol/BLE investigation may still be worthwhile if the architecture wants a local-first path.

This existing controller may significantly reduce the amount of additional fan/light actuator hardware needed for the first experiments.

Sources:

- https://github.com/lientry/homeassistant-vivosun-growhub
- https://vivosun.com/en/technical-guide/vivosun-growhub-controller-t143409044027744256
- https://vivosun.com/support/guide/growhub-e42a

---

## Milwaukee Instruments MC811 MAX

Status: **already owned; useful Hydroponics measurement source**.

The MC811 MAX continuously displays:

- pH;
- EC;
- temperature

on three large LCD displays.

The current manual documents the display/probes/power/calibration behavior but does not expose an obvious digital telemetry/API interface for integration.

### Cheap telemetry workaround: fixed camera node

A fixed ESP32/ESP32-S3 camera node can photograph the display at intervals and send frames or cropped regions to the backend.

Prefer:

`fixed camera → fixed display ROIs → dedicated digit/segment recognition → plausibility filtering → HA/system entities`

rather than relying only on unconstrained generic OCR.

Advantages:

- no modification of the MC811 MAX;
- avoids purchasing duplicate pH/EC probes just for telemetry;
- yields real pH/EC/temp data from the already trusted measurement device;
- camera can later be repurposed.

Validation requirements:

- compare extracted readings against manual visual readings;
- reject low-confidence/implausible values;
- detect stale/obscured display;
- never let one bad OCR reading directly trigger dangerous chemical dosing.

Potential camera candidates can be investigated separately; M5Stack and Seeed both offer inexpensive ESP32-S3 camera hardware.

Source:

- Milwaukee MC810/MC811 MAX manual:
  https://milwaukeeinstruments.eu/media/2b/fb/12/1733927478/mc810_811.pdf

---

# Priority A — highest value per Euro

## 1. M5Stack AtomS3 Lite as ESPHome / Bluetooth proxy / expandable node

Observed German pricing: about **€9.90** at BerryBase.

Why this is currently one of the strongest purchases:

- ESP32-S3;
- Wi-Fi + BLE;
- compact enclosure;
- USB-C;
- Grove/HY2.0 expansion;
- official/known ESPHome ecosystem support;
- can operate as a Home Assistant Bluetooth Proxy;
- can later host I²C sensors or other M5Stack Units.

Immediate use:

`TP357 BLE → AtomS3 Lite → dedicated 2.4-GHz IoT Wi-Fi → HAOS VM`

A single node could initially serve TP357 data and later be repurposed/extended.

ESPHome has both official Bluetooth-proxy projects and M5Stack-compatible configurations.

Sources:

- https://www.berrybase.de/m5stack/
- https://esphome.io/components/bluetooth_proxy/
- https://github.com/esphome/bluetooth-proxies
- https://docs.m5stack.com/en/homeassistant/

---

## 2. Shelly Plug M Gen3 — general-purpose mains actuator + power telemetry

Observed German price range: roughly **€12.90+** depending on seller/variant/shipping.

Relevant capabilities:

- 2.4-GHz Wi-Fi;
- Bluetooth;
- Matter;
- MQTT;
- switched mains output;
- power measurement;
- temperature/protection telemetry.

High-value uses:

- hydro circulation pump;
- air pump;
- fan;
- greenhouse light;
- test load;
- detecting whether a supposedly running load is actually consuming power.

This is currently preferable to a garden water-valve experiment because the owner does not have an obvious conventional outdoor water-tap use case and already has more relevant Hydroponics pumps.

Safety:

Only switch equipment within Shelly's documented electrical ratings and suitable load type. Do not treat nominal wattage alone as sufficient for inductive/motor loads.

Sources:

- https://www.shelly.com/
- https://geizhals.de/shelly-plug-m-gen3-a3779234.html

---

## 3. Window state sensor for greenhouse-room thermal logic

A window contact is genuinely useful for the room containing the greenhouse tents.

Desired automation/reasoning inputs:

- window closed/open/tilted;
- room temperature/humidity;
- tent temperature/humidity;
- outside temperature;
- sunlight/solar/weather conditions;
- wind where available.

Example reasoning:

Opening the window may help when outside air is materially cooler than the room/tents.

Opening it may be counterproductive when it is 30+ °C outside, sunny, and windless.

In winter, the same state can prevent excessive room cooling and help avoid greenhouse ventilation remaining suppressed for too long.

### Current attractive candidate: Shelly BLU Door/Window Mini ZB

Despite the `ZB` product name, this device supports **both Bluetooth 5 LE and Zigbee 3.0**, including simultaneous operation.

Current Shelly EU price observed: **€15.90**.

Relevant features:

- open/closed state;
- tilt/inclination;
- ambient-light measurement;
- Bluetooth BTHome;
- Zigbee available later if desired;
- up to five-year advertised battery life.

This is especially attractive because it can be used **BLE-only now**, through the same Home Assistant Bluetooth/BTHome + ESPHome proxy infrastructure as other BLE devices, while retaining a future Zigbee path.

Home Assistant's Shelly integration explicitly directs BLU devices to BTHome.

Sources:

- https://www.shelly.com/de/products/shelly-blu-door-window-mini-zb-white
- https://kb.shelly.cloud/knowledge-base/shelly-blu-door-window-mini-zb
- https://www.home-assistant.io/integrations/bthome/
- https://www.home-assistant.io/integrations/shelly

---

# Priority B — useful expansion after the basic loop works

## 4. Cheap light-state / relative-brightness sensor

The goal is **not horticultural-grade PPFD/PAR measurement**.

The useful first questions are:

- is the light actually on?
- did brightness change?
- is daylight contribution high/low?
- does measured light roughly match the commanded schedule?

### Minimal module: BH1750

Observed price: about **€2.40**.

### Easier M5Stack version: DLight Unit (BH1750)

Observed price: about **€6.50**.

Advantages of the M5Stack DLight path:

- prebuilt connector/module;
- quicker experiments;
- less breadboard wiring;
- easy attachment to an Atom/other M5Stack controller.

Do not interpret raw lux as grow-light PAR/PPFD.

Sources:

- https://www.berrybase.de/bh1750-digitaler-lichtsensor
- https://www.berrybase.de/m5stack/

---

## 5. M5Stack ecosystem for fast custom nodes

M5Stack is a particularly useful candidate ecosystem because many functions are available as small prebuilt Grove-compatible Units and Home Assistant/ESPHome documentation exists for numerous modules.

Interesting examples:

### AtomS3 Lite

~€9.90; useful base/controller/BLE proxy.

### ENV-IV

Temperature, humidity, pressure using SHT40 + BMP280; ESPHome components are documented by M5Stack.

This is less urgent because TP357 devices already cover temperature/humidity.

### DLight / BH1750

~€6.50; easy light-state/relative-brightness fixture.

### 2-channel relay Unit

Observed about **€7.50**.

Potentially useful for low-voltage control experiments when the exact load and electrical ratings are appropriate.

### 4-relay Unit

Observed about **€15.40**.

Useful if multiple isolated switching channels are needed.

### Watering Unit

Observed about **€14.50**.

Combines capacitive soil sensing and small-pump control.

This is more interesting for soil/substrate experiments than for the owner's current Hydroponics priority, but it is a cheap integrated actuator/sensor fixture.

Sources:

- https://docs.m5stack.com/en/homeassistant/
- https://docs.m5stack.com/en/homeassistant/components/sensor/unit_env_iv
- https://docs.m5stack.com/en/homeassistant/components/sensor/unit_watering
- https://www.berrybase.de/m5stack/
- https://www.berrybase.de/sensoren-module/m5stack-units/

---

## 6. Seeed XIAO ESP32-C6 Soil Moisture Sensor

Observed:

- Seeed official: about **US$10.90**;
- German OpenELAB listing: about **€14.85**.

Characteristics:

- XIAO ESP32-C6;
- Wi-Fi/BLE plus 802.15.4 capability;
- single-AA battery;
- Home Assistant compatibility;
- low-power soil monitoring.

This is a much cleaner productized soil sensor than a bare probe + development board.

However, soil/substrate sensing is currently lower priority than Hydroponics, so purchase can wait unless a soil-growing experiment needs it.

Sources:

- https://www.seeedstudio.com/XIAO-Soil-Sensor-p-6452.html
- https://wiki.seeedstudio.com/xiao_soil_moisture_sensor/
- https://openelab.de/products/seeed-studio-xiao-bodenfeuchtesensor

---

# Hydroponics control candidates

## 7. Main circulation / air / auxiliary pump control

For ordinary mains-powered pumps, the simplest first path is often:

`HAOS/System → Shelly Plug M Gen3 → existing pump`

Advantages:

- no custom mains wiring;
- easy manual override;
- power telemetry;
- reusable afterwards.

For low-voltage pumps/valves, use appropriately rated relay/MOSFET hardware rather than forcing every actuator through a mains smart plug.

M5Stack relay Units can be useful for low-voltage/control-side experiments, but exact voltage/current/load ratings must be verified for the target device before connection.

---

## 8. Dosing pumps — later and with safety interlocks

If peristaltic nutrient/pH dosing is added later, treat it separately from basic circulation pump control.

Minimum architecture expectations before autonomous chemical dosing:

- hard maximum dose per action/window;
- reservoir/flow plausibility;
- stale/invalid pH/EC reading rejection;
- manual override/emergency stop;
- calibration tracking;
- audit log;
- time for mixing before remeasurement;
- no direct actuation from one OCR value.

The initial Hydro experiment does **not** need autonomous pH dosing to prove the agent/control architecture.

---

# Weather-aware room/window logic

No dedicated outdoor sensor purchase is required for the first experiment.

Home Assistant weather integrations can initially provide external context such as:

- outside temperature;
- forecast;
- cloud/sun conditions;
- wind.

Combine with:

- room TP357;
- tent TP357 / VIVOSUN telemetry;
- window contact/tilt;
- light-state estimate;
- current fan/light states.

This provides a meaningful agent decision problem:

`Should opening/closing the window improve the thermal state right now?`

A physical outdoor temperature/weather sensor can later be added if internet weather data proves too coarse or poorly localized.

---

# Bluetooth architecture recommendation

Because several useful devices are BLE-based, a small Wi-Fi-connected ESPHome Bluetooth proxy is high-value.

Current preferred cheap candidate:

**M5Stack AtomS3 Lite**

Possible architecture:

`
TP357(s)
Shelly BLU Window
other future BLE sensors
        │
        ▼
AtomS3 Lite / ESPHome Bluetooth Proxy
        │  2.4-GHz IoT Wi-Fi
        ▼
HAOS VM
        │
        ▼
Home Assistant integrations / system modules
`

Home Assistant automatically aggregates supported ESPHome Bluetooth proxies with other Bluetooth adapters.

This also keeps the HAOS VM independent of a dedicated passed-through Bluetooth USB dongle for normal sensor reception.

---

# Revised suggested purchase order

Given the owner's already-owned hardware and current budget constraints:

1. **Buy nothing first:** integrate existing TP357 sensors and VIVOSUN E42A against HAOS.
2. **M5Stack AtomS3 Lite (~€9.90):** BLE proxy + expandable ESPHome node.
3. **Shelly Plug M Gen3 (~€12.90+):** universal actuator/power monitor; especially useful for Hydro pumps.
4. **Shelly BLU Door/Window Mini ZB (~€15.90):** use over BLE/BTHome now; Zigbee remains future option.
5. **BH1750 (€2.40) or M5Stack DLight (€6.50):** light on/off + relative brightness.
6. **Camera node for MC811 MAX:** choose once camera placement/image requirements are clearer.
7. **M5Stack relay/pump hardware:** only when a specific low-voltage pump/control target is chosen.
8. **XIAO ESP32-C6 Soil Sensor (~€10.90–14.85):** when soil/substrate experiments become relevant.
9. **Leak/water-level sensing:** choose based on actual Hydro reservoir layout.
10. **Zigbee coordinator + Zigbee-only devices:** later, when device count/value justifies the extra entry cost.

This sequence can start meaningful experiments with roughly **€10–40 of new hardware**, depending on how much is purchased initially, because the most valuable climate/controller devices are already owned.

---

# Purchase-status rule

Nothing in this file is assumed to be physically available to Implementation until the owner explicitly says it was purchased/received and adds it to the implementation input/inventory.

Already-owned devices explicitly stated by the owner are exceptions and should be tracked separately as existing test fixtures.

Do not copy this shopping shortlist into future-facing requirements documents merely because it exists.
