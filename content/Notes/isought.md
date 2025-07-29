---
title: Is–ought problems
date: 2025-07-29
tags:
   - philosophy
   - neuroscience
   - AI
---

In my essay critiquing [[Posts/neuroai.md | NeuroAI]], I took issue with the following statement:
> [!quote]
> The emerging field of NeuroAI, at the intersection of neuroscience and AI, is based on the premise that a better understanding of neural computation will reveal fundamental ingredients of intelligence and catalyze the next revolution in AI. \[1\]

My argument was that neuroscience is ill-positioned to advance AI because an algorithm’s similarity to the brain does not cause that algorithm to succeed in AI; an algorithm’s power and efficiency dictate its success, and these qualities might explain why the brain implements that algorithm. 

A particularly notable example concerns the declining popularity of recurrent neural networks (RNNs) in AI. Cortical circuits are highly recurrent, and RNNs explicitly mirror this feature. However, RNNs have since fallen out of fashion in favor of the (architecturally) non-recurrent Transformer. Therefore, an algorithm's similarity to the brain does not cause it to be successful in AI, nor is its similarity a good predictor of its success.

We can vaguely[^1] frame my argument as an ‘is-ought problem’. In David Hume’s A Treatise of Human Nature, Hume argues that one cannot validly derive normative statements (i.e., statements involving the word ‘ought’) from descriptive statements (i.e., statements involving the word ‘is’) \[2\]. For example, the following argument might seem flawed:
> [!example] Americans and taxes
> P1: Joe is an American.\
> P2: Most Americans pay taxes.
>
> <hr class="callout-sep">
>
> C1: Joe ought to pay his taxes.

Namely, the conclusion doesn’t logically follow from the premises. The premises are facts while our conclusion is normative. We could fix our logic by changing P2 to “Americans ought to pay taxes” or by adding a third premise “Citizens ought to follow the laws”. Simply put, descriptive statements (those involving “is”) don’t give us license to deduce normative statements (those involving “ought”).

Applying the is-ought framework to my critique on NeuroAI, we could write:
> [!example] The NeuroAI argument
> P3: The brain uses efficient algorithms.\
> P4: Algorithm $x$ resembles the brain.
>
> <hr class="callout-sep">
>
> C2: Algorithm $x$ ought to be an efficient algorithm.[^2]

In this view, P3 and P4 are facts, descriptive statements, while our conclusion is a prediction about the performance of the algorithm that appears to follow from our premises. While the argument looks enticing, what if we made the following argument regarding flight:
> [!example] Flying cars
> P5: Planes have chairs.\
> P6: Planes fly.\
> P7: Cars have chairs.
>
> <hr class="callout-sep">
>
> C3: Cars ought to fly.

Our logic above assumes that ‘chairs’ are sufficient for flight. Regarding our NeuroAI argument, we assume that ‘being brain-like’ is sufficient for being ‘an efficient algorithm’. Indeed, while algorithms 'being brain-like' could be correlated with ‘being efficient', our RNN example shows that this correlation is not causal.

Hence, by applying Hume’s is-ought framework to my critique of NeuroAI, we can see that the issue underlying NeuroAI is one of confusing correlation for causation. But why stop here? The following argument is also guilty of confusing correlation for causation:
> [!example] The reverse NeuroAI argument
> P8: The brain uses efficient algorithms.\
> P9: Algorithm $x$ is an efficient algorithm.
>
> <hr class="callout-sep">
>
> C4: Algorithm $x$ ought to be implemented in the brain.

Yet, as I described in my essay critiquing [[Posts/neuroai.md | NeuroAI]], the Kalman filter and Transformer algorithms are powerful algorithms that have yet to be concretely proven to be implemented in the brain.

So where do we go from here? How do we logically argue that the brain is implementing some algorithm? What Hume’s ‘is-ought problem’ tells us is that we have to appeal to normative statements in the premises of our arguments in order to deduce normative statements[^3]. For example, the following argument is much more reasonable:
> [!example] First principles of intelligence
> P10: The brain is an intelligent system.\
> P11: Intelligent systems ought to efficiently represent uncertainty.\
> P12: Algorithm $x$ most efficiently represents uncertainty over some class of algorithms $C$.
>
> <hr class="callout-sep">
>
> C5: The brain ought to implement algorithm $x$.

Since P11 is normative, we are more justified in making a normative conclusion about the relationship between algorithm $x$ and the brain.

The remedy to NeuroAI’s problem could be for researchers to appeal to **first principles**, like P11. Now rather than primarily cataloging implementation-level details of the brain, the bulk of NeuroAI could concern articulating, evaluating, and agreeing on what the first principles of intelligence are. This, I assume, is highly nontrivial.

## References

\[1\] Zador, A., Escola, S., Richards, B., Ölveczky, B., Bengio, Y., Boahen, K., ... & Tsao, D. (2023). Catalyzing next-generation Artificial Intelligence through NeuroAI. Nature Communications, 14(1), 1597.\
\[2\] Hume, D. (1985). _A Treatise of Human Nature_ (E. C. Mossner, Ed.). Penguin Classics.

[^1]: Let's emphasize the word 'vaguely' because our arguments will not always involve normative statements.

[^2]: Note, C2 is a predictive statement, not a normative statement. Hence, framing 'The NeuroAI argument' as an 'is-ought problem' is not entirely appropriate, but the framing is useful to identify the correlation/causation fallacy and we will employ Hume's reasoning at a later point.

[^3]: Now we see where Hume's 'is-ought problem' is useful in NeuroAI. It tells us to look for first principles of intelligence.