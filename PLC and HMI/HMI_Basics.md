# HMI and how to use HMI with PLC

## What is an HMI?
HMI (Human–Machine Interface) is the user interface that operators use to monitor and control machines and processes. HMIs provide visual displays (screens), inputs (buttons, touch), alarms, trends, logs, and operator actions (start/stop, setpoints).

## HMI functions
- Display process status (values, statuses, graphical mimic)
- Operator controls (pushbuttons, setpoint entry, recipes)
- Alarm and event management
- Trending and historical data logging
- Recipe management and operator authentication
- Diagnostics and maintenance screens

## HMI vs SCADA vs PLC
- PLC: real-time control and logic execution.
- HMI: operator interface for monitoring and control.
- SCADA: supervisory control + distributed data collection for larger systems (often includes HMI features).

## Typical HMI hardware/software
- Hardware: panel-mount touchscreens, industrial PCs, handhelds.
- Software: vendor HMI editors (e.g., Siemens WinCC, Rockwell FactoryTalk View, Schneider Vijeo), runtime on panels.

## Communication methods between HMI and PLC
- Ethernet/IP, Modbus TCP, Profinet, Modbus RTU (serial), Profibus, OPC UA, vendor-specific protocols.
- Choose protocol supported by both devices. Configure IP/baud/port and ensure proper cabling.

## Basic steps to use an HMI with a PLC
1. Plan
    - List required screens, tags, alarms, trends, recipes, operators.
    - Define PLC tags and data types needed by HMI.
2. Configure physical connection
    - Connect network or serial link, set IP addresses/baud rates.
3. Configure PLC
    - Create and name tags/variables for all items the HMI will read/write.
    - Arrange memory areas (coils, registers, data blocks) clearly.
4. Configure HMI project
    - Add communication driver and point it to PLC.
    - Create tags in the HMI that map to PLC variables (addressing or symbolic).
    - Design screens: indicators, pushbuttons, numeric entry, trends, alarm lists.
5. Implement scaling and data conversion
    - Apply linear scaling for raw registers (e.g., 0–32767 → 0–100%).
6. Configure alarms, trends, and recipes
    - Map alarm conditions to PLC or configure alarm logic in HMI.
    - Configure trend logging and recipe read/write if needed.
7. Security and user access
    - Define user roles, password levels, and logging of operator actions.
8. Test offline and online
    - Test HMI simulator, then test on the live system with PLC.
    - Verify read/write, response time, alarm behavior, and data accuracy.
9. Commission and maintain
    - Train operators, document tag list and screens, back up projects.

## Example (simple tag mapping)
- PLC tags:
  - Motor1.Run (BOOL)
  - Motor1.Fault (BOOL)
  - Motor1.SpeedSet (INT, raw 0–1000)
  - Motor1.SpeedRead (INT, raw 0–1000)
- HMI controls:
  - Start/Stop pushbuttons → write Motor1.Run
  - Fault lamp → read Motor1.Fault
  - Speed numeric entry → write Motor1.SpeedSet (with scaling: raw/10 → rpm)
  - Speed trend → read Motor1.SpeedRead

## Best practices
- Use descriptive tag names and keep a tag dictionary.
- Minimize polling traffic by grouping tags and adjusting scan rates.
- Keep HMI logic minimal; primary control logic belongs in PLC.
- Implement clear alarm priorities and concise messages.
- Secure network and HMI access; use VLANs and firewalls where appropriate.
- Version control HMI projects and maintain backups.

## Checklist before deployment
- Confirm protocol compatibility and cabling.
- Verify tag addresses and data types match PLC.
- Test read/write with simulator and on-device runtime.
- Validate alarms, trends, logging, and user permissions.
- Document configuration and operator instructions.