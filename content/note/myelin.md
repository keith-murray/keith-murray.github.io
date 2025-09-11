---
title: What does myelin do?
date: 2025-09-11
tags:
   - neuroscience
   - math
---

In class the other day, my professor was lecturing about the cellular components of a neuron when he turned to us, the students, and asked what purpose myelin served. Someone said the obvious answer that myelin insulates the axon, but then our professor asked a follow up question that surprised me: "Why does the axon need insulation?"

For some context, [myelin](https://en.wikipedia.org/wiki/Myelin) is a lipid-rich material oligodendrocytes produce to wrap around the axons of cortical neurons that project across the brain. Most people are familiar with the brain being composed of white and gray matter, and it's this myelin that gives white matter its color.

Coming back to my professor's question, I first thought of electrical insulation in circuits. We insulate wires so that exposed wires don't come into contact and short the circuit. But shorting is a property of pure electrical components and axons are electrochemical, so shorting is not a risk if unmyelinated axons come into contact. 

After a moment’s look at our blank faces, our professor said "Let's think back to the properties of a capacitor," and wrote on the board
$$
\Delta Q=C\Delta V,
$$
the equation for capacitance. The axonal membrane is modeled as a capacitor and can be described by
$$
C=\epsilon\frac{A}{d},
$$
where $A$ is the area of two capacitor plates and $d$ is the distance between them. Since the axonal membrane area doesn’t change much, the key difference is $d$, the effective thickness of the insulating layer. Myelination increases this distance $d$, causing a decrease in the capacitance of the cell membrane $C$.

For a neuron to fire, the voltage across the membrane spikes from $-70\ \text{mV}$ to $+30\ \text{mV}$, a total of $\Delta V = 100\ \text{mV}$. Given $\Delta Q = C\Delta V$, and noting that $C_\text{myelin} < C_\text{un}$, we get
$$
\Delta Q_\text{myelin}=C_\text{myelin}\Delta V<C_\text{un}\Delta V=\Delta Q_\text{un}.
$$
In other words, a myelinated axon requires less charge to fire than an unmyelinated one. 

Because less charge is needed, myelinated axons can propagate action potentials more quickly and efficiently. In short, from the basic properties of capacitors, my professor was able to show how myelination’s insulating effect helps axons propagate action potentials more efficiently. Pretty cool, right?