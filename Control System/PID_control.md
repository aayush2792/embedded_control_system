# PID control

PID (Proportional–Integral–Derivative) control is a classical feedback control method used to drive a process variable (PV) toward a desired setpoint (SP). The controller output is a weighted sum of three terms that react to the error $e(t)=\text{SP}-\text{PV}$:

$$
u(t) = K_p\,e(t) + K_i \int_0^t e(\tau)\,d\tau + K_d \frac{d e(t)}{dt}
$$

- Proportional ($K_p$): reacts to current error (reduces rise time).
- Integral ($K_i$): reacts to accumulated past error (eliminates steady-state error).
- Derivative ($K_d$): reacts to rate of error change (adds damping, reduces overshoot).

Discrete-time (sampled) form with sampling period $T_s$:

$$
u[k] = K_p e[k] + K_i T_s \sum_{i=0}^{k} e[i] + K_d \frac{e[k]-e[k-1]}{T_s}
$$

Practical tips and gotchas
- Integral windup: the integral term can grow unbounded when the actuator saturates. Mitigate with integral clamping, conditional integration, or back-calculation.
- Derivative noise: numerical derivative amplifies high-frequency noise. Filter the measurement or use a derivative-on-measurement with a small low-pass filter.
- Anti-windup and output limits: always clamp the controller output to actuator limits and stop integrating when saturated (or use a back-calculation term).
- Tuning: simple methods include Ziegler–Nichols or manual tuning (increase $K_p$ until oscillation, then set $K_i$/$K_d$); model-based tuning gives better results.
- Discretization: ensure consistent units and correct scaling of $K_i$ (often $K_i^\text{discrete}=K_i T_s$) and $K_d$ ($K_d^\text{discrete}=K_d/T_s$).

Minimal discrete implementation (pseudo-code):

```python
# Python-like pseudocode
Kp, Ki, Kd = ...
Ts = 0.01
integral = 0.0
prev_error = 0.0
for each sample:
    error = setpoint - measurement
    integral += error * Ts
    derivative = (error - prev_error) / Ts
    u = Kp*error + Ki*integral + Kd*derivative
    u = clamp(u, min_act, max_act)         # enforce actuator limits
    if u is at limit:
        integral = anti_windup_adjust(integral, u)  # e.g., stop integrating or back-calc
    prev_error = error
    apply(u)
