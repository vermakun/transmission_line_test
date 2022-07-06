# FTDR Intrusion Detection

The goal of this project is to define an itrusion localization method for known electrical networks.

This method should be extendable to black box networks, but for now we will focus on known networks in order to create a proof of concept.

Friendly ECUs will adjust their input impedance on a timed security frame in the network's messaging protocol and become identifiable and locatable using FTDR techniques.

# Transmission Lines

## 5.1 Introduction

Parallel, two wire systems.

Electric and magnetic field lines pass from one conductor to the other, creating inductive and capacitive effects.

Voltage and current are functions of distance along the line.

Focus on distributed-circuit theory and its relationship to field theory.

Two issues with transmission lines:
1. Poor impedance matching can cause reflections of signals.
2. Time delay is associated with dielectric material
3. Dipersion can cause smearing in the signal (frequency based velocity propogation)

## 5.2 Ideal Transmission Line

Assume a uniform parallel conductor, with distributed inducatance $L$ p.u. length and a distributed capacitance $C$ p.u. length.

The length $dz$ along this conductor has an inductance of $L \; dz$ and a capacitance of $C \; dz$.

<!-- <img src="img/intro_01.jpg" alt="Ideal t-line and euiv. circuit for a differential length."> -->

Following Kirchoff's Voltage Law, the voltage around this circuit loop rises by input voltage $V$, drops by  $-L \; dz \; \frac{\partial I}{\partial t}$, resulting in $V + \frac{ \partial V}{\partial z} dz$ on the output.

$$ \frac{\partial V}{\partial z} dz = -\left( L \; dz \right )\frac{\partial I}{\partial t} $$

Similarly, the change in current from input to output of the circuit is the current shunted across the distributed capacitance.

$$ \frac{\partial I}{\partial z} dz = -\left( C \; dz \right )\frac{\partial V}{\partial t} $$

We can simplify both equations by removing the common length term $dz$ from both sides.

$$ \frac{\partial V}{\partial z} = -L \; \frac{\partial I}{\partial t} $$

$$ \frac{\partial I}{\partial z} = - C \; \frac{\partial V}{\partial t} $$

In order to combine these two equations we find a common term $\partial^2 I / \partial z \partial t$:

$$ \frac{\partial^2 V}{\partial^2 z} = -L \; \frac{\partial^2 I}{\partial t \partial z} $$

$$ \frac{\partial^2 I}{\partial t \partial z} = - C \; \frac{\partial^2 V}{\partial^2 t} $$

With substitution, leading to:

$$ \frac{\partial^2 V}{\partial^2 z} = -L \; \left( - C \; \frac{\partial^2 V}{\partial^2 t} \right) $$

$$ \frac{\partial^2 V}{\partial^2 z} = LC \; \frac{\partial^2 V}{\partial^2 t}$$

This is a one-dimensional wave equation for voltage on a transmission line.

General solutions to this equation take the form:

$$ V(z,t) = F_1 (t - \frac{z}{v}) + F_2 (t + \frac{z}{v}) $$

Where $F_n$ are arbitrary functions (waves) that propogate the transmission line in either the +$z$ or -$z$ direction.

We can also find the current solution by subsituting $V(z,t)$ into our first voltage equation:

$$ - L \frac{\partial I}{\partial t} = \frac{\partial V}{\partial z} = -\frac{1}{v} F_1' (t - \frac{z}{v}) + \frac{1}{v} F_2 ' (t + \frac{z}{v}) $$

$$ I(z,t) = \frac{1}{Lv} \left[ F_1 (t - \frac{z}{v}) - F_2 (t + \frac{z}{v}) \right] + f(z)$$