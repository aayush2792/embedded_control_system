# Communication protocols — overview for PLCs

## What is a communication protocol?
A communication protocol is a defined set of rules and formats that devices use to exchange data reliably over a link or network. For PLC systems a protocol defines physical wiring/electrical/optical signals, message framing, addressing, timing/determinism and the application-level commands used to read/write I/O and configuration.

Important properties for PLC protocols:
- Determinism and real‑time behavior (bounded latency)
- Topology and medium (serial bus, Ethernet, wireless)
- Master/slave vs peer‑to‑peer architectures
- Throughput, cycle time and message size
- Interoperability and vendor support

## Common protocol families used with PLCs

### Serial / legacy
- Modbus RTU / Modbus ASCII — simple master/slave protocol over RS-232/RS-485. Very common for sensors, drives, small devices.
- DF1 (Allen‑Bradley), S7 PPI (Siemens) — vendor-specific serial links.

### Fieldbus (deterministic, device-level)
- Profibus DP — widely used with Siemens and many devices for fast I/O.
- DeviceNet — CAN-based network common for Allen‑Bradley ecosystems.
- CANopen — CAN-based fieldbus for motion, drives and distributed I/O.
- AS‑Interface (AS‑i) — simple low-cost I/O wiring for binary devices.
- CC‑Link, Interbus — region/vendor-specific fieldbuses.

### Industrial Ethernet (Ethernet-based, many real-time variants)
- EtherNet/IP — CIP-based, popular in Rockwell/Allen‑Bradley environments.
- PROFINET — Siemens/Profinet family supporting real‑time and isochronous modes.
- Modbus TCP — TCP/IP adaption of Modbus for Ethernet.
- EtherCAT — very low-latency, high-performance I/O & drive networks.
- POWERLINK, Sercos III — other real‑time Ethernet protocols.

### Higher-level / IT/IIoT protocols
- OPC UA — platform-independent data modeling and secure client/server (and Pub/Sub) for integration to SCADA/IT.
- MQTT, AMQP — lightweight publish/subscribe for IIoT telemetry (cloud/SCADA integration).

### Wireless
- WirelessHART, ISA100, Wi‑Fi, Bluetooth — used where cabling is impractical; typically for non-safety low-bandwidth data or monitoring.

## Choosing a protocol — practical guidance
- Small, low-cost I/O: AS‑i or Modbus RTU.
- Vendor-native systems (Siemens/Rockwell): PROFINET/EtherNet‑IP or their fieldbuses.
- High-performance motion or fast cyclic I/O: EtherCAT, EtherNet‑based real‑time variants.
- Plant-wide integration / historian / cloud: OPC UA / MQTT + gateway.
- Mix of legacy and modern: use protocol gateways/bridges (Modbus ↔ Ethernet, fieldbus couplers).

## Quick comparison (very high-level)
- Serial (Modbus RTU): simple, low cost, limited speed/determinism.
- Fieldbus (Profibus/DeviceNet/CANopen): deterministic, device-level standardization.
- Industrial Ethernet (Profinet/EtherCAT/EtherNet‑IP): high bandwidth, flexible topology, better integration with IT, some variants offer hard real‑time.