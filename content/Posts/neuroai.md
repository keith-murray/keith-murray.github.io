---
title: Critiquing NeuroAI
date: 2025-07-25
tags:
   - neuroscience
   - AI
---

## The promise of NeuroAI
Over the past five years, artificial intelligence (AI) has experienced one of the greatest waves of excitement and hype that any technology has ever seen—and it feels more than warranted. From my own experience, on December 4th, 2022, ChatGPT did my Real Analysis homework. I vividly remember the emotions running through my mind as I realized that ChatGPT had saved my night from the ‘MIT PSet grind’, as I realized ChatGPT would save many future nights from that grind.

So in light of the impact of AI, it’s worth asking, **how can we make AI better?** Some have provided the following answer:
> [!quote]
> Neuroscience has long been an essential driver of progress in artificial intelligence (AI). We propose that to accelerate progress in AI, we must invest in fundamental research in NeuroAI. \[1\]

This quote comes from the 2023 perspective paper titled “Catalyzing next-generation Artificial Intelligence through NeuroAI” where the authors, a mix of computer science and neuroscience academics, argue that advancements in neuroscience lead to advancements in AI, thus we should invest our resources in neuroscience to make better AI models and algorithms.

At first glance, it’s a promising idea given how most AI systems can be thought of as sophisticated deep *neural* networks. The word ‘neural’ is everywhere in AI[^1], so the proposal to advance AI with neuroscience appears to hold weight. However, it’s a superficial appearance; AI’s usage of the word ‘neural' is a remnant of the 40s and 50s when the first neural networks and associated learning algorithms were developed by neuroscientists. 

The history of technological advancements shows us that progress largely happens when engineers solve hard problems, and only afterwards do neuroscientists use this progress to formulate theories about the brain, not the other direction. From Sam Gershman’s 2024 perspective paper criticizing the claims of NeuroAI, he writes:
> [!quote]
> The strongest constraints on algorithms will always come from the structure of the problems that need to be solved, since engineers are paid to solve those problems rather than explain how the brain works. Happily, algorithms optimized for solving engineering problems frequently turn out to be successful models of brain function. \[2\]  

To support this argument of engineers inspiring neuroscientists, let’s investigate two examples:
1. The discovery of the Kalman filter by an electrical engineer, the algorithm’s refinement by aerospace engineers, and eventual adoption into neuroscience.
2. The discovery of the attention mechanism, the backbone of large language models (LLMs), by neuroscientists and the mechanism’s rediscovery and popularization by computer scientists.

## Kalman filter
Before examining the history of the Kalman filter, we need a working definition. However, complete explanations of the Kalman filter tend to devolve into a series of confusing, pronoun-laden sentences, as evidenced by [“The Missile Knows Where It Is”](https://www.youtube.com/watch?v=bZe5J8SVCYQ) internet meme. Therefore, let’s stick to the following overly simplified, yet comprehensible definition:
> [!info] Kalman filter
> The Kalman filter is a *recursive* algorithm used to estimate the evolving state of a dynamic system—such as an object’s position and velocity—from repeated, noisy measurements.  

I’ve emphasized the word ‘*recursive*’ as it is the most important feature of the algorithm and implies a computational advantage over alternative estimation algorithms.

The Kalman filter is named after the Hungarian-American electrical engineer Rudolf Kálmán, who proposed the algorithm in 1960 as an extension to the Wiener filter \[3\], another popular algorithm for signal estimation in noisy data. Unlike the Kalman filter, the Wiener filter operated on batches of stationary measurements, making it unsuitable for systems requiring continuous and instantaneous updates. Kalman’s work on *recursive* estimation methods expanded the scope and applicability of the Wiener filter’s ideas, but his novel probabilistic approach faced initial skepticism from colleagues. As a result, Kálmán had to publish his algorithm in a mechanical engineering journal rather than his typical electrical engineering venues.

Parallel to Kalman’s work, in 1959, the Dynamics Analysis Branch at NASA’s Ames Research Center was working on the problem of circumlunar guidance and navigation for what would become the Apollo program \[4\]. For context, a spacecraft in a circumlunar trajectory exits Earth’s orbit, flies to the Moon, slingshots around the Moon, flies back and lands on Earth. Spacecraft on such a trajectory need to make midcourse corrections to avoid crashing into the Moon or burning up in the Earth’s atmosphere upon landing. To understand when a spacecraft’s position deviated from the planned circumlunar trajectory, the Dynamics Analysis Branch was tasked with designing an on-board system to continuously estimate a spacecraft’s position and calculate its error relative to its desired trajectory.

To put it mildly, resources are limited in space; thus, the Branch had to design a navigational system with the following constraints in mind:

1. Accurate enough to satisfy restrictive entry corridor requirements on return to Earth.  
2. Semi-autonomous so as to require minimal input from onboard crew.  
3. Self-contained so as to not rely on communications with a satellite or ‘Houston’.  
4. Efficient enough to execute in a timely manner with onboard computers.

By the fall of 1960, the design of the system had been progressing smoothly. Differential equations were formulated to model the desired trajectory, an IBM 704 was selected as the on-board computer, and inertially referenced optical sensors were designed to measure the position of the spacecraft relative to the Earth and Moon. The primary issue, though, was how to relate the spacecraft's observed position to its desired trajectory so as to compute the error between the two.

The Branch was aware of the Wiener filter as a possible solution, as they had previously used it in designing the navigational systems for homing missiles[^2]. The Wiener filter could intake data from the optical sensors and output the error of the spacecraft's trajectory; however, the requirement for batched measurements of uniform size required constant input from crew onboard a spacecraft, violating the ‘semi-autonomous’ constraint. But in a serendipitous series of events, Kálmán came to the Branch, without knowledge of each other’s work, to present his algorithm that alleviated the Wiener filter’s restriction via *recursive* estimation, allowing for irregular and sparse input from the crew.

For the Branch, it was obvious that the Kalman filter satisfied their ‘semi-autonomous’ and ‘self-contained’ constraints, but they wouldn’t know about its accuracy or efficiency until they implemented the algorithm. Over the course of that winter, the team dedicated enormous resources to reformulate, extend, program, and simulate the Kalman filter, resulting in the Branch’s discovery of the even more popular *extended Kalman filtering algorithm*. By early 1961, the Branch had conclusive analytical and simulation evidence that the extended Kalman filter was the state-of-the-art in state-estimation algorithms for on-board navigation systems. Soon after publishing their results, the Kalman filter found widespread success in fields beyond the engineering of navigation systems, such as economics, robotics, and signal processing.

In 1995, nearly 35 years after its introduction, the success of the Kalman filter eventually found its way to cognitive science. Communicated in a *Science* publication, cognitive scientists at MIT discovered that the Kalman filter could predict the behavior of people performing a sensorimotor task \[5\]. Specifically, human participants were tasked with moving their limbs towards a goal location in a dark environment. It was found that the Kalman filter provided the best explanation for behavioral data collected during the task, showing how it’s plausible for the brain to perform a similar algorithm in moving its person’s limbs. In a way, these scientists were able to show that the problem of estimating one’s own hand as they pick up a glass of water is not unlike the problem of estimating the position of rockets as they travel to the moon.

Finally, in 2007, the insights of the Kalman filter flowed into neuroscience. Inspired by the findings from 1995, theoretical neuroscientists proposed a neural circuit that computes the Kalman filter algorithm \[6\]. Their key insight was that the *recursive* nature of the algorithm bears a resemblance to the *recurrent* connections of motor neurons. This similarity inspired the design of their neural circuit, and they further showed how their circuit explains a variety of previously puzzling data from motor neurons.

Before moving on to attention mechanisms, let’s briefly dwell on the similarity between the *recursive* nature of the Kalman filter and the *recurrent* connections of motor neurons. This similarity was not a motivating criteria for NASA engineers designing a navigation system; their criteria were solely the constraints of the problem and it was those constraints that identified the Kalman filter as their solution. Only after seeing the Kalman filter’s decades of success did neuroscientists notice its similarity to the brain, not the other direction. In other words, neuroscientists noticing an algorithm's similarity to the brain does not cause the algorithm to experience decades of success; an algorithm's power and efficiency dictate that success and it's these qualities that might explain why the brain implements that algorithm.

## Attention Mechanisms 
Given the success of LLMs, the word ‘attention’ has become a buzzword in the machine learning community, and buzzwords have a tendency to lose their original meaning. I say this as a caution to you, the reader, that my interpretation of attention mechanisms and their history may be different from your interpretation. In either case, whether you agree or disagree with my interpretation, my argument, that the popularization of the attention mechanism had nothing to do with neuroscience, is relevant.

An attention-like mechanism for deep neural networks was first proposed by neuroscientists in 1998 \[7\]. These researchers were interested in creating a model of visual saliency, in other words, a model of how visual features in our environment ‘jump out’. Their model was a convolutional neural network (CNN) that used the attention mechanism to magnify components of a picture that exhibited high-contrast. The model was reasonably successful at reproducing neural and behavioral phenomena of visual saliency in mammals, and became widely cited within neuroscience. Yet, the attention mechanism failed to be integrated into the broader machine learning community and was eventually neglected.

16 years later, in 2014, another attention-like mechanism was proposed by computer scientists developing machine translation models \[8\]. In machine translation, text from one language is translated to another, but given how grammatical rules vary across languages, computer models cannot simply translate text word-for-word. Instead, machine translation models in 2014 were built such that sentences were fed word-by-word as input, encoded into a *fixed-length* *vector*, and then decoded word-by-word into the desired language. These models implemented the aptly named “encoder-decoder” architecture, a *recurrent* architecture where each word was fed into or outputted from the model at each timestep. However, this method suffered when translating long sentences since the encoder had to cram the entire sentence into a *fixed-length* *vector*. 

To address this limitation, these 2014 computer scientists introduced an attention mechanism that removed the encoding of sentences into *fixed-length* *vectors* and allowed the model to focus on different parts of the input sentence dynamically during the decoding process. This mechanism enabled the handling of sentences of arbitrary length by reweighting the relevance of each input word when generating each output word. Note that these researchers did not take any inspiration from the neuroscientists 16 years before, but instead allowed the constraints of the problem, translating large sentences, and the drawbacks of the current methods, encoding into *fixed-length* vectors, to guide their rediscovery of the attention mechanism.

However, we don’t currently view attention mechanisms as a method for machine translation; we know them as the backbone of the transformer architecture and LLMs. 3 years after the attention mechanism’s rediscovery, the transformer architecture was introduced in the seminal paper “Attention Is All You Need” \[9\]. The transformer improved upon existing attention-augmented encoder-decoder architectures by removing *recurrency* entirely in favor of a large *feedforward* network of stacked attention mechanisms. Crucially, instead of inputting and outputting one word at a time, the transformer architecture took whole sentences as input and gave whole sentences as output. This new architecture not only beat existing machine translation benchmarks with a fraction of the training time, but also outperformed existing models on an English constituency parsing task. The researchers' dual results for the transformer architecture laid the seeds for future engineers to use a single model architecture for solving separate language tasks, instead of developing custom architectures for each task.

Less than a year later, in 2018, the first LLMs emerged. These LLMs, OpenAI’s GPT \[10\] and Google’s BERT \[11\], consisted of one transformer architecture pre-trained on a single language task and fine-tuned for a diverse range of language tasks. The approach of pre-training and fine-tuning models was not novel, but their use of the transformer architecture allowed for these approaches to beat state-of-the-art models that had been crafted for individual language tasks. Crucially, these engineering teams' decision to use the transformer architecture in building the first LLMs was not guided by the attention mechanism’s similarity to the brain; their decision was simply motivated by the architecture’s proven performance gains in a wide variety of language tasks. In short, transformers and attention mechanisms were used to build the first LLMs because they worked incredibly well, not because they were similar to the brain.

Following the widespread adoption of attention mechanisms in natural language processing, in 2021, cognitive scientists at MIT found evidence of the brain implementing the attention mechanism. Communicated in a *PNAS* paper, these cognitive scientists found that transformer models predicted nearly 100% of variance in neural activity across a broad range of language tasks and neural recordings, outperforming by far any other type of language model \[12\]. Like in the example of the Kalman filter, this study encouraged neuroscientists to once again theorize about the mechanistic underpinnings of the attention mechanism. In 2023, neuroscientists proposed that astrocytes, commonly thought of as a regulatory cell in the brain, could perform an attention-like computation \[13\], and recently, in 2024, neuroscientists proposed that short-term Hebbian plasticity, commonly thought of as a learning mechanism in the brain, could also perform an attention-like computation \[14\]. Given the relevance of the attention mechanism and the diverse range of biophysical mechanisms in the brain, neuroscientists are now just scratching the surface of theoretical implementations of attention in neural circuits.

As a final note on attention mechanisms, let’s examine what made the transformer architecture better than the previous encoder-decoder architectures. These encoder-decoder architectures were *recurrent* networks that had to store all relevant linguistic information in memory as words were fed in one-by-one. The transformer architecture, on the other hand, had no memory constraints since its *feedforward* nature allowed access to the entire sentence at once. It seems obvious that these *feedforward* networks would perform better than *recurrent* networks for language tasks, so why then were computer scientists and engineers previously focused on *recurrency*? 

There are a few answers to our question, but perhaps the most notable explanation for us is that these engineers were taking direction from the brain. The brain is highly *recurrent*, so it follows that our language networks are too. But, ironically, this brain-like feature, *recurrency*, was actually hindering the performance of these old networks\! The failure of *recurrency* in language models provides a salient example of how engineers taking direction from the brain can actually result in worse AI. This example becomes even more interesting by considering that *recurrency* was a desirable property in the Kalman filter\! Thus we have to ask, what value does an algorithm's resemblance to the brain bring to engineers solving difficult problems?

## A critique of NeuroAI
With the Kalman filter and attention mechanism examples in mind, let’s look at the following quote from the NeuroAI paper:
> [!quote]
> The emerging field of NeuroAI, at the intersection of neuroscience and AI, is based on the premise that a better understanding of neural computation will reveal fundamental ingredients of intelligence and catalyze the next revolution in AI. \[1\]  

But as our Kalman filter and attention mechanism examples show, insights into intelligence are not simply “revealed” through a better understanding of the brain. 

I argue that the discovery of “fundamental ingredients of intelligence” happens in two parts:
1. The insight is discovered.  
   - In the case of Kalman filtering, by an electrical engineer.  
   - In the case of the attention mechanism, by a group of neuroscientists.  
2. The insight is recognized and refined through engineers working under nontrivial constraints.  
   - In the case of Kalman filtering, this was an enormous effort by a NASA engineering team, which led to the development of the wildly successful extended Kalman filter.  
   - In the case of the attention mechanism, the mechanism was rediscovered by computer scientists and extended to the wildly successful transformer architecture by engineers not afraid to abandon recurrence.

To NeuroAI’s credit, neuroscience can play a role in proposing insights. As I noted before, neural networks and learning algorithms were orignially formulated by neuroscientists attempting to model the brain, and there may still be more insights that we can port from neuroscience to AI. However, discovering insights into intelligence is the relatively[^3] easy part. The hard part of understanding intelligence can only be played by the engineer solving hard problems with nontrivial constraints. In short, **my critique with NeuroAI is that it does not accurately depict progress towards understanding intelligence; therefore, it cannot prescribe a process for how to develop better AI**.

Furthermore, neuroscientists don’t even take their own insights into intelligence seriously. The attention mechanism example shows how neuroscientists renewed attention[^4] to the mechanism was not because it was a good idea proposed 25 years ago. Neuroscientists are now interested in the attention mechanism because engineers proved that it’s incredibly useful in building LLMs and cognitive scientists showed that these mechanisms are likely to exist in the brain. This reinforces my earlier point that **neuroscientists noticing an algorithm's similarity to the brain does not cause the algorithm to experience decades of success; an algorithm's power and efficiency dictate that success and it's these qualities that might explain why the brain implements that algorithm.**

This particular flaw in the practice of neuroscience is best expressed by Jerrome Lettvin who wrote in the Forward to the 1988 reissue of Warren McCulloch’s *Embodiments of Mind*:
> [!quote]
> To a greater degree than in any other current science, we must know what to look for in order to recognize it. Precisely here is the deficit in neuroscience. We can observe the results of processing in the behavior of animals and in records taken from individual neurons, but we cannot account for either by mechanism. This is where a prior art is needed, some understanding of process design. And that is where AI, PDP, and the whole investment in building \[neurocomputational models of intelligence\] enter in. Critics carp that the current golems do not resemble our friends Tom, Dick, or Harry. But the brute point is that a working golem is not only preferable to total ignorance, it also shows how processes can be designed analogous to those we are frustrated in explaining in terms of nervous action. It suggests what to look for. \[15\]

And now, in 2024, our current “golems” are starting to bear a strong resemblance to “our friends Tom, Dick, and Harry”.

In the context of the Kalman filter, engineers showed how to build systems that can infer their own state and, most importantly, explained *why* systems *should* infer their state. The engineers' normative reasons around the computation of the Kalman filter consequently inspired cognitive scientists to hypothesize about whether humans infer their own state, and neuroscientists to theorize about what neural mechanisms might be responsible for this computation. In the context of attention mechanisms, engineers showed how models built around these mechanisms vastly outperform all other models and, again most importantly, explained *why* these mechanisms are *naturally suited* for language tasks. These explanations then motivated cognitive scientists to hypothesize about whether humans’ language networks perform attention-like computations, and neuroscientists to theorize about what neural mechanisms might be responsible for this computation.

## The upshot
So what now? In light of my arguments that neuroscience doesn’t drive AI, what is the role of neuroscience? What can neuroscience bring to the AI table?

Just as Gershman articulated the main flaw of NeuroAI, he also articulates an answer to our questions above in the same paper:
> [!quote]
> Instead of looking for inspiration, a more plausible (but weaker) heuristic is to look for convergence: If engineers propose an algorithm and neuroscientists find evidence for it in the brain, it is a pretty good clue that the algorithm is on the right track (at least from the perspective of building human-like intelligence). \[2\]  

Essentially, neuroscience can provide an important feedback signal about progress towards “building human-like intelligence”.

In the Kalman filter and attention mechanism examples, I described a flow of ideas from the formulation of an idea, to its development by engineers, to the hypotheses of cognitive scientists, and finally to the theorizing of neuroscientists. But there's one last step: experimental neuroscientists collecting data that confirms those theories. It’s this experimental step that fully confirms that the original idea is essential to biological intelligence; it’s this step that demonstrates *convergence* between the engineer’s algorithm and the brain’s mechanisms. I didn't document this last step in my Kalman filter and attention mechanism examples because, to my surprise, we’ve yet to find conclusive evidence for an implementation of the Kalman filter or attention mechanism in the brain.

While I can understand the excitement of proposing entirely novel theories of intelligence, there’s also an excitement around collecting data and proving, or disproving, those theories. Imagine the flip side of experimentation; imagine if we can’t find evidence of the attention mechanism’s implementation in the brain. Sure, one could blame the theoretical neuroscientist for not theorizing the correct implementation or the experimental neuroscientist for not using a precise enough method. Or, one could take the bold leap and accept that the brain is doing something more clever than the attention mechanism. Isn’t that exciting? Isn’t it thrilling to think that we can build such powerful and intelligent LLMs, but our brains might be smarter because experimental neuroscientists couldn’t find evidence for their implementation.

Convergence may be a “weaker” heuristic than inspiration, but it’s just as exciting, if not more. As I’ve stated before, proposing theories of intelligence is 'relatively' easy since any field, from mathematics to computer science and neuroscience can do it. Recognizing and explaining why a theory is fundamental to intelligence is significantly harder and occupies the mind of the engineer. But if our goal is to understand the brain and what makes it *generally intelligent* from a *mechanistic perspective*, then there is no alternative to the experimental neuroscientist doing the hard work and looking for what might be in the brain.

**References**

\[1\] Zador, Anthony, et al. "Catalyzing next-generation artificial intelligence through NeuroAI." *Nature communications* 14.1 (2023): 1597\.  
\[2\] Gershman, Samuel J. "What have we learned about artificial intelligence from studying the brain?" *Biological Cybernetics* 118 (2024): 1-5.  
\[3\] Kalman, Rudolph Emil. "A new approach to linear filtering and prediction problems." *Journal of basic Engineering* 82.1 (1960): 35-45.   
\[4\] McGee, Leonard A., and Stanley F. Schmidt. *Discovery of the Kalman filter as a practical tool for aerospace and industry*. No. NASA-TM-86847, 1985\.  
\[5\] Wolpert, Daniel M., Zoubin Ghahramani, and Michael I. Jordan. "An internal model for sensorimotor integration." *Science* 269.5232 (1995): 1880-1882.  
\[6\] Deneve, Sophie, Jean-René Duhamel, and Alexandre Pouget. "Optimal sensorimotor integration in recurrent cortical networks: a neural implementation of Kalman filters." *Journal of neuroscience* 27.21 (2007): 5744-5756.  
\[7\] Itti, Laurent, Christof Koch, and Ernst Niebur. "A model of saliency-based visual attention for rapid scene analysis." *IEEE Transactions on pattern analysis and machine intelligence* 20.11 (1998): 1254-1259.  
\[8\] Bahdanau, Dzmitry, et al. "Neural machine translation by jointly learning to align and translate." *arXiv preprint arXiv:1409.0473* (2014).  
\[9\] Vaswani, Ashish, et al. “Attention Is All You Need.” *arXiv preprint arXiv:1706.03762* (2017).  
\[10\] Radford, Alec et al. "Improving language understanding by generative pre-training." (2018).   
\[11\] Devlin, Jacob et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." *arXiv preprint arXiv:1810.04805* (2018).  
\[12\] Schrimpf, Martin, et al. "The neural architecture of language: Integrative modeling converges on predictive processing." *Proceedings of the National Academy of Sciences* 118.45 (2021): e2105646118.  
\[13\] Kozachkov, Leo, Ksenia V. Kastanenka, and Dmitry Krotov. "Building transformers from neurons and astrocytes." *Proceedings of the National Academy of Sciences* 120.34 (2023): e2219150120.  
\[14\] Ellwood, Ian T. "Short-term Hebbian learning can implement transformer-like attention." *PLOS Computational Biology* 20.1 (2024): e1011843.  
\[15\] McCulloch, Warren S. *Embodiments of mind*. MIT press, 1988\.

[^1]:  Except of course, for the name ‘artificial intelligence’.

[^2]:  God bless America’s military industrial complex (this is sarcasm).

[^3]:  I don't mean to say that discovering some insight into intelligence is 'easy'; discovery in any context is difficult. I mean to say that discovering insights is easier than solving large engineering problems.

[^4]:  Well that’s meta.