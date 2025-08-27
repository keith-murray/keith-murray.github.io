---
title: Beyond falsifiability
date: 2025-08-07
tags:
   - neuroscience
   - philosophy
   - language
---

Despite the brain’s (quite literally) central position in our lives, our understanding of the brain is still very much in its infancy. We have no universal theory of brain function and scientists routinely disagree about how one [[note/isought.md | ought]] to approach brain research. In light of this lack of theory, some researchers are going back to the basics of science and advocating for neuroscience research centered around falsifiable theories and hypotheses.

This grounding of neuroscience research in falsifiability echoes the work of philosopher Karl Popper in demarcating science from pseudoscience via the _Criterion of Falsifiability_:
> [!info] Criterion of Falsifiability
>
> Science is the study of falsifiable theories and hypotheses.

Since [Popper’s 1959 book](https://psycnet.apa.org/record/1961-02882-000) _The Logic of Scientific Discovery_ where he proposed this criterion, it’s been widely noted that plenty of scientific statements and theories are unfalsifiable. While a complete synopsis of the problems of a “falsifiable” conception of science deserves its own [[index.md | post]], I’ll briefly outline in this note one particular example from [Scott Soames’s book](https://www.jstor.org/stable/j.ctt7t1cs) _Philosophical Analysis in the Twentieth Century_:
> [!note] Proposition 1
>
> For every substance, there is a solvent.

Breaking proposition 1 down into its logical form, we have
$$
\forall x (Sx \rightarrow \exists y\, D(x,y)).
$$
If one chemist were to utter **Proposition 1** to another chemist, they would understand each other and agree that **Proposition 1** is a valid scientific claim. Now suppose an ambitious chemist were to go about falsifying **Proposition 1**. They would need to find a substance such that there is no solvent; however, the issue is that the space of possible solvents (i.e. chemical compounds) is infinite. Thus, while **Proposition 1** is in principle falsifiable, it is practically unfalsifiable: Popper’s _Criterion of Falsifiability_ doesn’t distinguish tractible scientific theories from intractable theories.

We can actually take this example and apply it to neuroscience:
> [!note] Proposition 2
>
> For every behavior, there is a subset of neurons responsible for that behavior.

Breaking **Proposition 2** down into its logical form, we have
$$
\forall x (Bx \rightarrow \exists y\, (y\subseteq N\, \&\, R(y,x))).
$$
Notice how the logical form of **Proposition 2** resembles that of **Proposition 1**, and just like **Proposition 1**, if one neuroscientist were to utter **Proposition 2** to another neuroscientist, they would understand each other and agree upon its validity. One difference, though, is that the number of subsets of neurons (for a particular animal/human) is finite. However, if we assume that the human brain is comprised of 100 billion neurons, then the size of the powerset of 100 billion neurons is $2^{100 \text{ billion}}$, which is intractable. Thus, while **Proposition 2** is in principle falsifiable, it is in practice unfalsifiable and we run into the same issue with Popper’s criteria as **Proposition 1**.

This all goes to show that neuroscience needs more than falsifiable theories and hypotheses. While falsifiability can be a useful heuristic, it isn’t a necessary requirement towards formulating _tractable_[^1] theories and hypotheses of the brain.

[^1]: However, it might not be possible that we can formulate _tractable_ theories of the brain.