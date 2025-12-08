---
layout: post
title: "Exploring Bias, Radicalization, and Human Choice in AI Recommender Systems"
date: 2025-12-01
author: "José Guilherme Loureno Correia Marques dos Santos, Francisco José Gomes da Silva, Mateus Maria Gomes Eça de Queiroz Cabral, Victor Daniel Tóms Rodriguez"
categories: [Machine Learning, Recommender Systems, AI Ethics]
tags: [algorithms, bias, radicalization, matrix factorization, regulation, YouTube]
excerpt: "Recommender systems quietly shape what we watch, read, and listen to. This article explores how these systems can amplify political bias and nudge users toward extremism, combining technical analysis with empirical evidence."
---

## Abstract

Recommender systems quietly shape what we watch, read, and listen to. On platforms like YouTube, they decide which video auto-plays next and which topics follow us across sessions. This article explores how these systems, particularly YouTube's recommendation algorithm, can amplify political bias and even nudge users toward more extreme content. Combining a matrix-factorization-based simulation with recent empirical audits and counterfactual studies, we argue that recommendation algorithms are not neutral tools but design artefacts that reflect business incentives, data biases, and societal power structures. We conclude by discussing how regulation, technical design choices, and informed user behaviour can work together to steer these systems toward more democratic outcomes.

---

## 1. Why Recommender Systems Matter Today

### 1.1 A Polarized World Curated by Algorithms

Artificial intelligence recommender systems have fundamentally transformed how individuals discover and consume information. YouTube, the most popular video platform globally, is a prime example. With around 81% of the U.S. population using the platform and about 70% of watch time driven by algorithmic recommendations, YouTube's recommender has become one of the most influential information gatekeepers in contemporary society.

This power operates in a context of deep political polarization. The gap between left and right on key issues has widened, hostility between partisan groups has increased, and support for political violence is not negligible. Social media and recommendation algorithms are regularly accused of locking users into filter bubbles and leading them down rabbit holes of increasingly ideological or conspiratorial content. YouTube, in particular, has been labelled "the great radicalizer," a platform whose algorithmic logic allegedly pushes users from mainstream content toward increasingly extreme material.

### 1.2 The Core Question: Are Algorithms Driving Radicalization?

At the heart of the debate lies a deceptively simple question: do recommendation algorithms systematically direct users toward extreme, conspiratorial, or otherwise problematic content?

Answering this requires unpacking what we call the **loop effect**, a feedback cycle with four interacting components:

1. **Selective exposure**: Users tend to consume information that matches their pre-existing views.
2. **Homophily**: Social networks, online and offline, are biased toward like-minded connections.
3. **Filter bubbles**: Personalization algorithms learn from this biased behaviour and recommend more of the same.
4. **Feedback**: As users follow these recommendations, their future options and sometimes their beliefs become more homogeneous.

Empirically, the picture is complex. Large-scale audits report that YouTube's algorithm favours ideologically congenial content and that this effect is especially strong for right-leaning users. More recent counterfactual studies, however, suggest that after major algorithmic changes in 2019, user preferences may play a larger role than algorithmic bias, with recommendations sometimes moderating rather than radicalizing viewing behaviour. Reality lies somewhere in between: algorithm and user co-produce the information environment.

### 1.3 Key Stakeholders in This Ecosystem

Several actors shape and are shaped by these algorithms:

| Stakeholder | Role | Incentives & Constraints |
|---|---|---|
| **YouTube/Google** | Platform operator | Optimizes for engagement and advertising revenue; profit-driven prioritization of attention-capturing content |
| **Users** | Content consumers | Most consume mainstream content; small, highly engaged subset encounters extreme material; preferences directly train models |
| **Creators** | Content producers | Respond to platform incentives; provocative, emotionally charged content often performs better, reinforcing supply |
| **Regulators** | Governance bodies | EU Digital Services Act (DSA) requires transparency and non-personalized alternatives; first serious regulatory attempt |
| **Researchers** | Knowledge producers | Develop auditing methods (sock-puppet experiments, counterfactual bots) to isolate algorithmic influence from user choice |

---

## 2. How Modern Recommender Systems Work

### 2.1 From Click Logs to Latent Factors

At their core, recommender systems predict which items a user is likely to appreciate based on historical interaction patterns. On YouTube, the items are videos; on Netflix, they are movies or series; on Spotify, songs and playlists. A central technical paradigm for this prediction task is **matrix factorization**, which starts from a large user-item interaction matrix **R**, where each entry $r_{ui}$ might represent a rating, a view, or another engagement signal.

Matrix factorization assumes that both users and items can be embedded into a lower-dimensional latent space. Formally, we approximate:

$$R \approx UV^T$$

where **U** is a matrix of user latent factors and **V** is a matrix of item latent factors. The dot product between a user's and an item's latent vectors approximates the strength of their interaction.

On platforms like YouTube, this idea is instantiated across several surfaces:
- **Homepage recommendations**: What users see when they open the site
- **Up-next recommendations**: What auto-plays after the current video
- **Search-based suggestions**: Results tailored to user history

Each surface can use slightly different models or weighting strategies.

### 2.2 Design Choices That Create Feedback Loops

YouTube's recommender reflects a set of optimisation choices:

1. **Objective function**: Engagement metrics such as watch time, click-through rate, and session length are primary targets.
2. **Personalization**: Models are trained on each user's history and the behaviour of similar users.
3. **Heterogeneous surfaces**: Homepage and up-next recommendations are tuned differently, with homepage often being more strongly personalized.

Combined, these choices create the loop effect. If a user repeatedly watches content from a particular political leaning, the model updates that user's latent vector towards that region of the space and increases the score of similarly positioned videos. Over time, the user's local neighbourhood in latent space can become ideologically homogeneous, even if the global catalogue is diverse.

### 2.3 Our Simulation: Matrix Factorization in a Political Toy World

To make these dynamics concrete, our project implements a recommender simulation based on the MovieLens 100K dataset. While MovieLens is about movies, not politics, it provides a clean, well-understood environment to prototype algorithms.

#### Dataset and Political Mapping

The original dataset contains 100,000 interactions over 31 attributes. For experimentation, we select a subset of 50 users and 100 movies, including a focal user with ID 196. We then map 19 movie genres into three political categories:

| Category | Genres | Count |
|---|---|---|
| **Neutral** | Comedy, Animation, Children's, Musical, Drama, Romance, Sci-Fi, Fantasy, Documentary, Unknown | 10 |
| **Mildly Political** | Action, Adventure, Thriller, Crime, Mystery | 5 |
| **Extreme** | War, Film-Noir, Horror | 3 |

This mapping is obviously stylized but serves as a proxy to observe how an algorithm shifts a user's recommendations along a neutral–extreme axis.

#### Simulation Parameters

We train models with the following configuration:
- **Users**: 50
- **Movies**: 100
- **Latent dimension**: $k = 10$
- **Simulation rounds**: 5 (for observing drift)
- **Learning rate**: 0.30

---

## 3. What We Learn from Outcomes and Implications

### 3.1 The Upside: Navigation, Personalization, Scale

It is important to acknowledge that recommender systems deliver genuine value:

**Navigation**: They help users navigate enormous catalogues. Without some form of algorithmic triage, platforms like YouTube would be nearly unusable.

**Personalization**: Good recommendations surface content that users might never have found manually. For many, this is experienced as serendipity rather than manipulation.

**Scalability**: Matrix factorization and related methods allow platforms to operate at web scale, computing recommendations for millions of users and items in near real-time.

### 3.2 The Downside: Filter Bubbles and Radicalization Pathways

Yet these very mechanisms also have serious downsides:

**Filter bubbles for politically engaged users**: While most users see a relatively mixed information diet, politically active partisans are more likely to inhabit echo chambers, both in their social networks and their recommender-driven feeds. This small group is often more vocal, more politically engaged, and more influential than average citizens.

**Algorithmic radicalization pathways**: Empirical evidence shows that some users move from centrist to more extreme channels over time. Our simulation shows the mechanism: when the model updates user factors after every extreme click, the latent profile shifts in that direction, and so do future recommendations.

**Right-leaning asymmetry**: Multiple audits find stronger amplification of congenial and problematic content for right-leaning users than for left-leaning ones. This asymmetry is not yet fully understood, but may relate to different content supply patterns across the ideological spectrum, the higher engagement provoked by certain right-wing narratives, or incomplete enforcement of platform policies.

**Normalisation through exposure**: Even if 97.5% of recommendations do not point to problematic channels, the fact that over a third of users eventually encounter such channels somewhere in their recommendation trails matters. Repeated incidental exposure can gradually shift what counts as normal or acceptable.

### 3.3 Opacity and Accountability Gaps

From the outside, YouTube's recommender is effectively a black box. Researchers can log what is recommended and what gets watched, but cannot directly see the internal model structure or objective functions. This opacity has several consequences:

- Platforms can claim that certain policy changes (e.g., reducing borderline content) had large positive effects without independent verification.
- Users cannot meaningfully understand or contest why specific items are recommended.
- Regulators struggle to assess systemic risks or enforce standards.
- Causal responsibility for harms becomes hard to attribute.

### 3.4 A Supply-and-Demand Perspective

A helpful way to cut through the algorithm vs. users dichotomy is to adopt a **supply-and-demand lens**:

- **Supply**: Extremist and conspiratorial creators produce content that is engaging to certain audiences, sometimes financially rewarded through monetization.
- **Demand**: Users with pre-existing grievances, prejudices, or curiosity seek out or dwell on such content.
- **Matching**: Recommender systems optimised for engagement become increasingly efficient at connecting this supply and demand.

In this view, the algorithm amplifies and structures existing dynamics rather than creating them ex nihilo. Effective interventions therefore need to address:
- **Supply** (e.g., moderation, demonetization)
- **Demand** (e.g., media literacy, social support)
- **The matching mechanism** (e.g., recommender design and constraints)

---

## 4. Why This Matters for Society and Governance

### 4.1 Media Narratives and Platform Responses

High-profile journalism has played a major role in framing YouTube as a radicalizing force. Stories like "The Making of a YouTube Radical" (New York Times) and essays such as Zeynep Tufekçi's "YouTube, The Great Radicalizer" cast recommender systems as almost autonomous agents driving individuals toward extremism.

In response to mounting criticism, YouTube announced a **Four Rs policy framework**:

1. **Remove**: Content that clearly violates policies.
2. **Raise up**: Authoritative sources in recommendations.
3. **Reward**: Trusted, policy-compliant creators.
4. **Reduce**: The spread of borderline content (videos that do not quite violate rules but are considered harmful).

YouTube claims these measures significantly reduced views of borderline content, but independent verification is limited due to black-box constraints.

### 4.2 Regulation: The Digital Services Act and Beyond

The European Union's **Digital Services Act** directly targets recommender systems. Key requirements include:

- Platforms must describe the main parameters of their recommender systems in plain and intelligible language.
- Very large online platforms must provide at least one non-profile-based recommendation option (e.g., chronological ordering).
- Regulators receive stronger auditing and data access powers.

The EU's **AI Act**, while not ultimately categorising recommenders as high-risk systems, further signals regulatory concern about opaque, large-scale algorithmic systems.

### 4.3 Challenging the Myth of Algorithmic Neutrality

The idea that algorithms are neutral, objective tools is increasingly untenable. Design decisions embed human values at multiple levels:

**Objective choice**: Engagement optimisation vs. accuracy, diversity, or civic value.

**Preference modelling**: Users are treated as isolated individuals rather than socially embedded agents whose preferences evolve.

**Content ranking**: Default favouring of popular or trending items can systematically marginalise minority viewpoints.

**Training data**: Historical patterns of inequality and discrimination are reproduced in model behaviour.

These are not mere implementation details—they are normative choices with political and ethical consequences.

### 4.4 Agency, Determinism, and Time

Counterfactual bot studies remind us that users retain significant agency. Many radicalization trajectories involve users actively searching for, subscribing to, or repeatedly selecting extreme content. The algorithm is complicit but not omnipotent.

At the same time, the effects of recommenders change over time. Pre-2019 YouTube likely behaved differently from the post-2019 version. This means that empirical results must always be interpreted in temporal context:

- Platform changes can and do alter outcomes, which is evidence that different designs are possible.
- Long-term research and monitoring are essential to track the impact of both platform self-regulation and formal regulation.

### 4.5 Fairness and Asymmetry

The persistent asymmetry whereby right-leaning users receive stronger amplification of congenial and problematic content raises fairness concerns. At minimum, it suggests that the recommender does not treat all political orientations equivalently. Possible contributors include:

- Higher density of right-wing alternative media on YouTube
- Different engagement patterns across audiences
- Uneven moderation or enforcement practices

Regardless of exact causes, such asymmetries challenge claims of neutrality and highlight the need for fairness-aware recommender research.

---

## 5. Takeaways: Steering Recommender Systems Toward Better Futures

Putting all the pieces together, recommender systems on platforms like YouTube are best understood as **socio-technical infrastructures**—they are neither neutral tools nor all-powerful puppet masters. Instead, they are powerful amplifiers shaped by business models, design decisions, data flows, and user behaviour.

### Key Takeaways

1. **Algorithmic bias is real but not the whole story**. Recommenders can and do amplify ideological bias and occasionally promote problematic content, yet user preferences and broader social dynamics remain crucial.

2. **Design choices matter**. Objective functions, model architectures, and ranking heuristics embed values. Post-2019 algorithm changes on YouTube demonstrate that different trade-offs can be made.

3. **Transparency and governance are essential**. Regulatory frameworks like the DSA, combined with independent auditing, are needed to make recommender systems accountable rather than opaque.

4. **Multiple levers must be pulled**. Effective responses must combine supply-side moderation, demand-side education, design changes (e.g., diversity-promoting objectives), and user empowerment tools.

5. **Education helps**. Interactive simulations and visualisations allow students, policymakers, and the wider public to see how seemingly abstract algorithms can produce concrete social patterns.

### Final Reflection

Recommender systems will remain central to digital life. The question is not whether we use them, but whose values they encode, whose interests they serve, and how we collectively govern them. This work—combining technical understanding, empirical evidence, and critical reflection—is essential for building AI systems that serve democratic values rather than undermine them.

---

## References

[1] Haroon, M., Wojcieszak, M., Chhabra, A., Liu, X., Mohapatra, P., Shafiq, Z. (2023). "Auditing YouTube's recommendation system for ideologically congenial, extreme, and problematic recommendations." *Proceedings of the National Academy of Sciences*, 120(50).

[2] CS8 Project Proposal (2025). "Exploring Bias, Radicalization, and Human Choice in AI Recommender Systems."

[3] Haroon, M., Chhabra, A., Liu, X., Mohapatra, P., Shafiq, Z., Wojcieszak, M. (2022). "YouTube, The Great Radicalizer? Auditing and mitigating ideological biases in YouTube recommendations." *arXiv*, 2203.10666.

[4] Whittaker, J. (2022). "Recommendation Algorithms and Extremist Content: A Review of Empirical Evidence." GIFCT Transparency Working Group.

[5] Hosseinmardi, H., Ghasemian, A., Rivera-Lanas, M., Ribeiro, M. H., West, R., Watts, D. J. (2023). "Causally estimating the effect of YouTube's recommender system using counterfactual bots." *Proceedings of the National Academy of Sciences*.

[6] Koren, Y., Bell, R., Volinsky, C. (2009). "Matrix factorization techniques for recommender systems." *IEEE Computer*, 42(8), 30–37.

[7] Raza, S., et al. (2024). "A Comprehensive Review of Recommender Systems." *arXiv*.

[8] Tufekçi, Z. (2018). "YouTube, The Great Radicalizer." *The New York Times*.

---

## About This Article

This article is part of the "Artificial Intelligence and Society" course at Faculdade de Ciências and Faculdade de Engenharia, Universidade do Porto. It represents a collaborative analysis of how recommendation algorithms shape information ecosystems and explores pathways toward more equitable and transparent algorithmic governance.

**Interactive Demonstration**: An interactive Streamlit application accompanying this research is available at [your-streamlit-app-url]. The application allows users to explore matrix factorization dynamics and visualize how algorithmic recommendations shift as users interact with content across the ideological spectrum.

---

*Last updated: December 8, 2025*
