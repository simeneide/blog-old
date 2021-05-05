---
title: "Dynamic Slate Recommendation with Gated Recurrent Units and Thompson Sampling"
layout: post
categories: [recsys]
---
Very excited to present "Dynamic Slate Recommendation with Gated Recurrent Units and Thompson Sampling" by @freeges , @DLeslieLancs and myself: A bandit-based Bayesian NN that recommends slates of items.
We also release a dataset that includes the items presented to the user.
https://arxiv.org/abs/2104.15046

The model uses a new (and in our view more realistic) likelihood (slate likelihood) and uses Thompson Sampling to explore and show a diverse set of items to the user in each slate. To tackle the cold-start problem, we use hierarchical item priors. We test both offline and online.

Along with our paper, we release a recommender systems dataset from the Norwegian marketplace FINN.no that not only includes the sequence of the user's clicks (or not clicked), but also what items the user was shown in each slate.
https://github.com/finn-no/recsys-slates-dataset

This is important because recsys often assume that the user considers all items on a platform, while they in reality only choose from a smaller slate presented to them. With this new dataset, we are able to make more reasonable models about user behaviour!

We compare these two different forms of likelihood (slate vs allitem likelihood), and find both theoretically and empirically that the new "slate likelihood" is (surprisingly?) not always better.

In fact, if the slates shown to the user on the platform are mostly search slates (above 80%), the all-item likelihood actually performs better. This is because it is biased to recommend the same items that has been already presented to the user.

We also present a new exploration&diversity technique that samples from the posterior distribution on each slate presented to the user (in-slate thompson sampling). This ensures exploration, but it also gives a diversity to the slate that increases click rates in real world experiments.

There is of course more to the paper than this. Check it out here :)
https://arxiv.org/abs/2104.15046
https://github.com/finn-no/recsys-slates-dataset