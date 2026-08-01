---
title: Is scale enough?
date: 2026-07-31
tags:
   - neuroscience
   - AI
---

Before I started my PhD in Neuroscience, a friend asked what I thought about Richard Sutton’s “[The Bitter Lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)” essay and if it made me second guess my decision to do a PhD. For context, Sutton’s Bitter Lesson can be described by the following statement:
> [!info] The Bitter Lesson
>
> Historically, general purpose models that continue to scale with increased computation have also tended to overtake more specialized domain-specific approaches.

In the context of doing a PhD in Neuroscience, I was originally motivated by the promise of NeuroAI:
> [!info] Promise of NeuroAI
>
> By developing a better understanding of the brain, we can build better AI agents.

There are a number of [[post/neuroai.md | critiques against the NeuroAI promise]], but Sutton’s lesson gives us another one:
> [!note] The Bitter Lesson critiques NeuroAI
>
> Any biological insight used to build better AI will eventually be beat by a general purpose model that can scale.

Given The Bitter Lesson is a historical argument, we can look for examples of a general purpose model that beat a biologically motivated model. Perhaps the best example is how transformers usurped recurrent neural networks (RNNs) as the favored model for natural language processing. RNNs were originally designed to mimic the recurrence of neural circuits in the brain; however, they had issues with gradient stability at scale. Transformers, in contrast, did not have a gradient stability issue and, more to Sutton’s point, could scale very well, leading to them being selected for natural language processing.

But, as evidence that I kept my decision to pursue a PhD, I was unconvinced by this argument. My thinking was that “Surely evolution must have settled upon some superior architecture? Why can’t we look to evolution as a means of sidestepping the discovery process?” In the context of transformers and RNNs, we could save face by saying, “Well, it’s not going to be easy to decipher evolution's solutions”. Importing recurrence wholesale is probably more complicated than previously thought, but once we understand how the brain stably learns with recurrence, we could design an RNN architecture that beats the transformer.

Hence, in the first year of my PhD, I set out to defend my decision to pursue a PhD in Neuroscience by formulating a counterargument to Richard Sutton’s Bitter Lesson. More specifically, I attempted to find a counterargument that “scale was not all you need” to build better AI agents.

I found inspiration for this counterargument in an introduction to neuroscience lecture given by Michael Graziano. The argument goes as follows:
> [!example] Vision and The Bitter Lesson
> P1: When solving a task, evolution ought to use existing biological mechanisms that already solve the task rather than evolve entirely new mechanisms.\
> P2: Our early vertebrate ancestors had dedicated neural circuits and brain areas responsible for vision.\
> P3: These visual circuits evolved into the superior colliculus.\
> P4: The telencephalon, which develops/evolves into the neocortex, did not evolve for vision.\
> P5: At some point in evolution, some vertebrates (which later evolved into mammals) co-opted the telencephalon for vision.
>
> <hr class="callout-sep">
>
> C1: If “scale is all you need”, evolution ought to have scaled-up the superior colliculus instead of co-opting the telencephalon.

Expressing my counterargument as a question, why did evolution go through this seemingly painful process of redeveloping vision circuits in the telencephalon when it already had a head start in the colliculus? If scale is all you need, shouldn’t we expect the superior colliculus to have expanded and further evolved?

Excited that I had successfully developed a counterargument to Sutton’s Bitter Lesson, I brought it to my advisor who openly admits that he takes Sutton’s Lesson very seriously. His response was simple:
> [!question] My advisor's response
>
> Doesn’t the neocortex fold?

Let’s unpack this. If you look at the human brain, the most striking feature is the gyrification of the neocortex. In the beginning of Graziano’s lecture on the superior colliculus, he began with a few remarks about what makes the neocortex different from the brainstem. In these remarks, he stated something like the following[^1]:
> [!note] Neocortex and the skull
>
> The neocortex is folded in order to allow more of the cortical sheet to fit within the skull.

Combining my advisor's response and Graziano’s explanation, we get the following:
> [!note] Neocortex scales in the skull
>
> The structure of the neocortex allows it to scale within the human skull.

Or equivalently:
> [!note] Teleological neocortex
>
> The neocortex is designed to scale.

What Daw did was flip my counterargument on its head and use it as an argument for Sutton’s Bitter Lesson: the superior colliculus wasn’t selected for in evolution because it couldn’t scale; therefore, evolution co-opted a brain area that could scale to meet the expanding demands of the visual world.

Now looking back at Sutton’s Bitter Lesson, it’s clear where I went wrong. I misinterpreted the lesson as “scale is all you need”. Instead, it says that general purpose methods that can scale are very powerful. In light of the superior colliculus and the neocortex, it’s simple: the superior colliculus is not general purpose and/or poorly scales, but the neocortex is general purpose and can scale. While my original counterargument is moot, we might be able to salvage it:
> [!note] The brain is not the neocortex
>
> If scaling general purpose methods is all we need for intelligence, why isn’t the brain entirely composed of the neocortex?

The neocortex is intimately connected to the hippocampus, basal ganglia, thalamus, cerebellum, and spinal cord, and if the Bitter Lesson is to be taken literally, shouldn’t evolution have discarded these areas in favor of the neocortex? Of course, these are normative claims, and the Bitter Lesson isn’t making a normative point, nor is evolution guaranteed to be an optimal process, but the question suggests that there must be something more to biological intelligence than general purpose methods that scale.

At the end of my first year, I’m thinking back to my friend’s original question: if I care about building better AI, does Sutton’s Bitter Lesson make me reconsider my decision to pursue a PhD in Neuroscience? While I’ve attempted to argue that there is more to biological intelligence than The Bitter Lesson, it’s now clear to me that scaling general purpose methods plays a key role. To answer my friend’s question, no, Sutton’s Bitter Lesson doesn’t make me reconsider my decision to pursue a PhD, but yes, it does make me reconsider what I should study for my PhD.

At the end of his essay, Sutton concludes with the following two sentences:
> [!info] Sutton's conclusion
>
> We want AI agents that can discover like we can, not which contain what we have discovered. Building in our discoveries only makes it harder to see how the discovering process can be done.

The wrong objective might be to build in what we have discovered biology is capable of; instead, a better objective might be to understand how biology discovers, and then model AI agents that discover like biology.

[^1]: As a side note, this is a [[note/irony.md | teleological]] explanation and some philosophers of science would argue that this is not a valid explanation in biology, but what makes a valid explanation in biology is a topic for another time.