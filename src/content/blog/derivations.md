---
title: 'Derivations'
description: 'Derivations'
pubDate: 'Mar 21 2026'
heroImage: '../../assets/blog-placeholder-2.jpg'
---

Equation 7 in [Bhagatwala, 2015](#references) is the following

$$
\begin{aligned}
\dfrac{\partial \rho}{\partial t} & = - \dfrac{\partial \rho u_i}{\partial x_i} + \dot{m} \\
\dfrac{\partial \rho u_i}{\partial t}  & = - \dfrac{\partial \rho u_i u_j}{\partial x_i} 
- \dfrac{\partial P}{\partial x_i} + \dfrac{\partial \tau_{ij}}{\partial x_i} + \dot{m}u_i \\
\dfrac{\partial \rho e_t}{\partial t}  & = - \dfrac{\partial \rho e_t u_j}{\partial x_i} 
- \dfrac{\partial P u_j}{\partial x_j} + \dfrac{\partial \tau_{ij}u_i}{\partial x_j} 
- \dfrac{\partial q_j}{\partial x_j} + \dot{m}e_t \\
\dfrac{\partial \rho Y_k}{\partial t}  & = - \dfrac{\partial \rho Y_k u_j}{\partial x_i} 
- \dfrac{\partial J_{k,j}}{\partial x_j} + \omega_k + \dot{m}Y_k \\
\end{aligned}
$$

and equation 8 is the following

$$
P(\mathbf{x}, t) = P_t(t) + p(\mathbf{x}, t) = \rho \mathrm{R} T 
$$

According to [Bhagatwala, 2015](#references), upon differentiating equation 8 and using equation 7, the rate of change of pressure is determined to be

$$
\dfrac{\partial P}{\partial t} = (\gamma - 1) \bigg(
\dfrac{\partial \rho e_t}{\partial t} - 
u_i\dfrac{\partial \rho u_i}{\partial t} +
\dfrac{u_i^2}{2}\dfrac{\partial \rho}{\partial t} -
\sum_{k} h_k \dfrac{\partial \rho Y_k}{\partial t}
\bigg) 
+ \gamma \mathrm{R_u} T \sum_{k} \dfrac{1}{W_k} \dfrac{\partial \rho Y_k}{\partial t}
$$

which is equation 9 in his paper. In this section I will derive the equation 9 from equation 7 and equaiton 8.
Let's start with the equation of state.

$$
P = \rho \mathrm{R} T
$$

Let's write temperature in terms of internal energy

$$
\begin{aligned}
T & = \dfrac{e}{C_\mathrm{v}} \\
P & = \rho \mathrm{R} \dfrac{e}{C_\mathrm{v}} \\
P & = \rho e \dfrac{\mathrm{R}}{C_\mathrm{v}} \\
& = \rho e \dfrac{C_\mathrm{p}-C_\mathrm{v}}{C_\mathrm{v}} \\
& = \rho e \bigg(\dfrac{C_\mathrm{p}}{C_\mathrm{v}} - 1\bigg) \\
& = \rho e \big(\gamma-1\big) \\
\end{aligned}
$$

Differentiating both sides.

$$
\dfrac{\partial P}{\partial t} = 
\big(\gamma-1\big) \bigg( \rho\dfrac{\partial e}{\partial t} +
e\dfrac{\partial \rho}{\partial t} \bigg) +
\rho e\dfrac{\partial}{\partial t} \big(\gamma-1\big)
$$

Now lets express internal energy in terms of total internal energy and kinetic energy

$$
e=e_\mathrm{t} - \frac{u_i u_i}{2}
$$

$$
\begin{aligned}
\dfrac{\partial P}{\partial t} 
& = \big(\gamma-1\big) 
\bigg(e_\mathrm{t}\dfrac{\partial \rho}{\partial t} - \frac{u_i u_i}{2}\dfrac{\partial \rho}{\partial t} + \rho\dfrac{\partial e_\mathrm{t}}{\partial t} - \rho\dfrac{\partial u_i u_i/2}{\partial t} \bigg)
+ \rho e\dfrac{\partial \gamma}{\partial t} \\
& = \big(\gamma-1\big) 
\bigg(e_\mathrm{t}\dfrac{\partial \rho}{\partial t} + \rho\dfrac{\partial e_\mathrm{t}}{\partial t} - \frac{u_i u_i}{2}\dfrac{\partial \rho}{\partial t} - \rho\dfrac{\partial u_i u_i/2}{\partial t} \bigg)
+ \rho e\dfrac{\partial \gamma}{\partial t} \\
& = \big(\gamma-1\big) 
\bigg(\dfrac{\partial \rho e_\mathrm{t}}{\partial t} - \frac{u_i u_i}{2}\dfrac{\partial \rho}{\partial t} - \rho\dfrac{\partial u_i u_i/2}{\partial t} \bigg)
+ \rho e\dfrac{\partial \gamma}{\partial t} \\
\end{aligned}
$$

### References

Bhagatwala, A. (2015). On the representation of chemistry in low Mach number reactive flows. *Combustion and Flame*, 162(6), 2108-2123. https://doi.org/10.1016/j.combustflame.2015.06.005