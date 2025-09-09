---
title: What does myelin do?
date: 2025-09-09
tags:
   - neuroscience
---

In class the other day, [Prof. Sam Wang](https://en.wikipedia.org/wiki/Sam_Wang_(neuroscientist)) was lecturing about the cellular components of a neuron when he turned to us, the audience, and asked what purpose myelin served. Someone said the obvious answer about how myelin insulates the axon of the neuron, but then Prof. Wang asked a follow up question that surprised me: "Why?"

For some context, myelin is a lipid-rich material oligodendrocytes produce to wrap around the axons of cortical neurons that project across the brain. Most people are familiar with the brain being composed of white and gray matter, and it's this myelin that gives white matter its color.

Coming back to Prof. Wang's question, "Why is insulating the axon of the neuron desirable?" In my mind, I first thought of electrical insulation in circuits. We insulate wires so that exposed wires don't come into contact and short the circuit, but shorting is a property only of pure electrical components. Brain signals are of an electrochemical nature, so shorting is not a risk if unmyelinated axons come into contact: my first thought led me down a dead end.

What surprised me even more was that moments after Prof. Wang asked the question, his eyes grew wide and he lowered his head in contemplation; he seemed to have forgotten the answer to his own question. He then raised his head, said "Let's think back to the properties of a capacitor," and wrote on the board
$$
\Delta Q=C\Delta V,
$$
the equation capacitance.

His explanation took the following form:

> [!example] Myelin decreases charge required for action potential
> P1: The equation for capacitance is $\Delta Q=C\Delta V$.\
> P2: The voltage required for an action potential is fixed at $\Delta V=30\text{mv}-(-70\text{mv})=100\text{mv}$.\
> P3: The capacitance for unmyelinated axons is greater than myelinated axons $C_\text{un} >C_\text{myel}$.
>
> <hr class="callout-sep">
>
> C1: The amount of charge required to achieve an action potential is less in myelinated axons than in unmyelinated axons $\Delta Q_\text{myel} = C_\text{myel}\Delta V < C_\text{un}\Delta V = \Delta Q_\text{un}$.

In essence, myelinated axons require less charge to propagate an action potential than unmyelinated axons, and this results in quicker and more energy-efficient action potential propagation[^1].

What struck me about Prof. Wang's explanation is how it's a simple explanation rooted in basic scientific principles, enabling Prof. Wang to construct it on the fly. In fact, it's so elegant that nobody noticed that it's incomplete.

While it's true that myelination lowers the capacitance of axons, myelination leaves gaps called ["nodes of Ranvier"](https://en.wikipedia.org/wiki/Node_of_Ranvier) that enable [saltatory conduction](https://en.wikipedia.org/wiki/Saltatory_conduction), whereby action potentials propagate down the axon in discrete, quick jump. In reality, it's this saltatory conduction that is the main enabler of quick and energy efficient action potential propagation, not the decrease in capacitance.

Despite this flaw, I’m still a fan of Prof. Wang’s explanation. It shows how powerful simple logic and basic scientific principles can be. My first thought about electrical insulation was misleading, but if I’d abstracted one level deeper, to the principles of circuits, I might have landed on capacitance myself.

[^1]: Note that this explanation relies on an assumed understanding that the distance between two plates of a capacitor is inversely proportional to its capacitance $C\propto\frac{1}{d}$.
