# PLC — Programmable Logic Controller

## What is PLC
A PLC (Programmable Logic Controller) is an industrial, ruggedized digital computer used to automate electromechanical processes (machines, factory lines, robots, building systems). It is designed for real‑time control in harsh environments.

## Core functions
- Read discrete/analog inputs (sensors, switches, transducers)  
- Execute a user program (control logic) deterministically  
- Update outputs (relays, motors, valves, actuators)  
- Provide diagnostics, timing, counting and communication

## Main hardware parts
- CPU / processor  
- Power supply  
- Input/output (I/O) modules (digital and analog)  
- Communication ports (Ethernet, serial, fieldbuses like Modbus, Profibus)  
- Memory and storage  
- Programming HMI / engineering workstation

## How it works (scan cycle)
1. Read inputs  
2. Execute program logic once (deterministic)  
3. Update outputs  
4. Run diagnostics/communications  
Cycle repeats continuously (scan time depends on program and CPU).

## Common programming standards & languages
IEC 61131‑3:
- Ladder Diagram (LD) — widely used in discrete control  
- Function Block Diagram (FBD) — reusable blocks, good for analog/process control  
- Structured Text (ST) — high‑level, text‑based (like Pascal)  
- Sequential Function Chart (SFC) — for sequence tasks  
(Instruction List (IL) is deprecated)

## Typical applications
- Manufacturing and assembly lines  
- Motion and robotics control  
- Process industries (chemical, water, food)  
- Building automation (HVAC, lighting)  
- Machine safety and test rigs

## Advantages
- Rugged, reliable, and real‑time deterministic control  
- Modular and scalable I/O  
- Wide vendor/tool support and standards compatibility  
- Easy maintenance and diagnostics for technicians

## Simple logic example (conceptual)
- If Start = ON and Stop = OFF then Motor = ON else Motor = OFF

This provides a concise overview suitable for an introductory PLC document.