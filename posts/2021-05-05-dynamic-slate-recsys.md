---
aliases:
- /recsys/2021/05/05/dynamic-slate-recsys
categories:
- recsys
date: '2021-05-05'
image: assets_old/interaction_illustration.png
layout: post
title: Dynamic Slate Recommendation with Gated Recurrent Units and Thompson Sampling

---

Authors: Simen Eide, David S. Leslie, Arnoldo Frigessi
Publication: Data Mining and Knowledge Discovery
Preprint: 5 May 2021
Publication: 19 July 2022

Paper link: 
[https://link.springer.com/content/pdf/10.1007/s10618-022-00849-w.pdf](https://link.springer.com/content/pdf/10.1007/s10618-022-00849-w.pdf)

Code link:
[https://github.com/finn-no/recsys-slates-dataset](https://github.com/finn-no/recsys-slates-dataset)

![](assets_old/interaction_illustration.png)


## Abstract

We consider the problem of recommending relevant content to users of an internet platform in the form of lists of items, called slates. We introduce a variational Bayesian Recurrent Neural Net recommender system that acts on time series of interactions between the internet platform and the user, and which scales to real world industrial situations. The recommender system is tested both online on real users, and on an offline dataset collected from a Norwegian web-based marketplace, this http URL, that is made public for research. This is one of the first publicly available datasets which includes all the slates that are presented to users as well as which items (if any) in the slates were clicked on. Such a data set allows us to move beyond the common assumption that implicitly assumes that users are considering all possible items at each interaction. Instead we build our likelihood using the items that are actually in the slate, and evaluate the strengths and weaknesses of both approaches theoretically and in experiments. We also introduce a hierarchical prior for the item parameters based on group memberships. Both item parameters and user preferences are learned probabilistically. Furthermore, we combine our model with bandit strategies to ensure learning, and introduce `in-slate Thompson Sampling' which makes use of the slates to maximise explorative opportunities. We show experimentally that explorative recommender strategies perform on par or above their greedy counterparts. Even without making use of exploration to learn more effectively, click rates increase simply because of improved diversity in the recommended slates.

