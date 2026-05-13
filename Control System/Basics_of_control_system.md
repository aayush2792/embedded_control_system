# Basics of a Control System

A control system is a set of components that manage, command, direct, or regulate the behavior of other devices or systems to achieve a desired output. Typical goals are to make the system stable, accurate, fast, and robust to disturbances and modeling errors.

## Key components
- Plant: the physical system to be controlled (motor, temperature loop, aircraft).
- Controller: computes control actions (PID, state-feedback, MPC).
- Sensor: measures outputs (position, temperature).
- Actuator: applies the controller's commands to the plant (valve, motor).
- Reference (setpoint) and Disturbances: desired value and unwanted inputs.

## Open-loop vs Closed-loop
- Open-loop: controller does not use measurement feedback.
- Closed-loop (feedback): controller uses sensor feedback to correct errors.

## Modeling (brief)

Common models:

### Time-domain ODE

$$
m \ddot{x} + b \dot{x} + kx = F(t)
$$

### Transfer function

$$
G(s)=\frac{X(s)}{F(s)}=\frac{1}{ms^2+bs+k}
$$

### State-space

$$
\dot{x}=Ax+Bu,\quad y=Cx+Du
$$

## Typical analysis goals
- Stability (will the response remain bounded?)
- Time-domain specs: rise time, settling time, overshoot
- Frequency-domain specs: gain/phase margins, bandwidth
- Robustness to model uncertainty and noise

## Common controllers & design tools
- PID (Proportional–Integral–Derivative): simple and widely used.
- Root-locus, Bode plots, Nyquist: classical frequency/graphical methods.
- State-feedback, LQR, Kalman filter: modern state-space methods.
- Model Predictive Control (MPC): optimization-based for constraints.

## Simple example (PID idea)
If plant is $G(s)$ and controller is $C(s)$, closed-loop transfer from reference $R(s)$ to output $Y(s)$ is

$$
T(s)=\frac{C(s)G(s)}{1 + C(s)G(s)}.
$$

## Gotchas and practical concerns
- Modeling error and unmodeled dynamics (flexible modes, actuator limits)
- Sensor noise and filtering trade-offs (delay vs noise reduction)
- Time delays can destabilize closed-loop systems
- Nonlinearities may invalidate linear design assumptions

### Example applications

- ## Example applications

### Room thermostat (temperature regulation)

- Description: maintain indoor temperature despite weather and occupancy changes.

- Simple model:

$$
C\frac{dT}{dt}=-\frac{(T-T_{\mathrm{amb}})}{R}+Q_{\mathrm{in}}
$$

- Measurement and drive: thermometer for feedback, heater/AC as the actuator.

- Typical controller: bang–bang with hysteresis or a PID-like regulator to reduce steady-state error.

---

### Automotive cruise control (speed maintenance)

- Description: hold vehicle speed under varying slopes and loads.

- Simplified dynamics:

$$
m\frac{dv}{dt}=-bv+u
$$

- where \(u\) is propulsion force.

- Sensing and actuation: speed sensor (wheel encoder) and throttle actuator.

- Typical controller: PI or state-feedback; feedforward for slope compensation.

---

### DC motor speed/position control

- Description: regulate rotational speed or position of a shaft.

- Electrical dynamics:

$$
L\frac{di}{dt}+Ri+K_b\omega=V
$$

- Mechanical dynamics:

$$
J\frac{d\omega}{dt}+B\omega=K_t i-\tau_{\mathrm{load}}
$$

- Hardware: encoder for position/speed, H-bridge or driver for voltage/torque.

- Typical controller: cascaded PI (current loop + speed/position loop) or full-state feedback.

---

### Inverted pendulum on a cart (balancing)

- Description: stabilize an unstable upright equilibrium and move the cart to a target.

- Model: nonlinear pendulum dynamics linearized about upright for controller design.

- Sensors/actuators: angle encoder/IMU and a horizontal force actuator on the cart.

- Typical controller: LQR or pole-placement for stabilization, sometimes augmented with observers.

---

### Liquid-level control in a tank

- Description: keep a liquid level constant despite fluctuating inflow.

- Model:

$$
A\frac{dh}{dt}=q_{\mathrm{in}}-q_{\mathrm{out}}(h)
$$

- often nonlinear outflow, or linearized integrator.

- Instrumentation: level sensor and control valve on inflow or outflow.

- Typical controller: PI or MPC when interacting with other process constraints.

---

### Quadcopter attitude control

- Description: maintain desired roll, pitch, and yaw angles during flight.

- Dynamics: rotational inertia and torques from propellers; coupling between axes.

- Sensors/actuators: IMU (gyros/accel) and variable-speed motors.

- Typical architecture: cascaded PID or model-based controllers with rate and angle loops.

---

### Magnetic levitation (maglev) stage

- Description: suspend and position a ferromagnetic object without contact.

- Dynamics: strongly nonlinear relation between coil current and magnetic force.

- Sensing and actuation: position sensor and coil current driver.

- Typical controller: nonlinear control or linearized feedback with observers for robustness.

---

### Chemical reactor temperature control (CSTR)

- Description: regulate reactor temperature to ensure reaction performance and safety.

- Features: strong nonlinearities and time delays; heat removal via coolant flow.

- Actuation and sensing: thermocouples and coolant valve/pump.

- Typical controller: PID for simple loops, MPC when constraints and interactions are important.