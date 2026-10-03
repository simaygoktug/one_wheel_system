# One Wheel System: PID Control

Modelling of a damped rotating wheel and PID controller design by matching a desired closed-loop characteristic equation, simulated in MATLAB.

## Overview

A wheel with moment of inertia $J$ and rotational damping $C$ is driven by a torque $T$. The task (MKT3822 Lab 3, Application 3, Yildiz Technical University) is to derive the equation of motion, obtain the transfer function and state-space model, choose PID gains that place the closed-loop poles at $s = -5, -10, -15$, and simulate tracking of a sinusoidal reference.

## Modelling

Summing moments about the wheel axis:

$$J\ddot{\theta} + C\dot{\theta} = T$$

which gives the plant transfer function from torque to angle

$$G_p(s) = \frac{1}{J s^2 + C s}$$

## Controller design

With the PID controller $C(s) = K_p + K_i/s + K_d s$ in unity feedback, the closed-loop transfer function is

$$G_{cl}(s) = \frac{K_d s^2 + K_p s + K_i}{s(J s^2 + C s) + K_d s^2 + K_p s + K_i}$$

The desired characteristic equation is

$$(s+5)(s+10)(s+15) = s^3 + 30s^2 + 275s + 750$$

With $J = 1$ and $C = 30$, matching coefficients gives $K_d = 30 - C = 0$, $K_p = 275$ and $K_i = 750$. The closed-loop system is simulated with the reference

$$r(t) = 5 + 2\sin(2\pi f t), \qquad f = 0.1 \text{ Hz}$$

over 100 s using `lsim`.

## Repository structure

```
.
├── one_wheel_system.m                           # Empty placeholder (0 bytes)
├── one_wheel_system.mat                         # Saved workspace: J, C, Kp, Ki, Kd, f, t, r, y
└── 22067606_LAB3_GR1_AR3_GöktuğCan-Şimay.pdf    # Lab report: derivation, block diagram, gain selection, MATLAB code, response
```

## How to run

Requires MATLAB with the Control System Toolbox.

`one_wheel_system.m` is currently empty. The simulation code is listed in Part 4 of the lab report; it can be pasted into a script and run. Alternatively, the saved results can be plotted directly:

```matlab
load one_wheel_system.mat
plot(t, r, 'b--', t, y, 'r-'); grid on
xlabel('Time (seconds)'); ylabel('Output')
legend('Reference Signal', 'System Output')
```

## Results

The closed-loop response to the sinusoidal reference is shown in the lab report PDF, and the simulated time series (`t`, `r`, `y`) are stored in `one_wheel_system.mat`.

## Author

Goktug Can Simay ([GitHub](https://github.com/simaygoktug) | [Website](https://goktugcansimay.com))
