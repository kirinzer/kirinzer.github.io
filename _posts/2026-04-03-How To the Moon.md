---
layout: post
title: How "To the Moon" and "Endgame" Led Me to Build a Decision Audit Engine
date: 2026-04-02
categories: Tech
cover: '/assets/img/to-the-moon.webp'
tags: Dev Design
english: true
---

## How "To the Moon", "Avengers: Endgame", and a Question About Regret Led Me to Build a Decision Audit Engine

> *Not to eliminate regret, but to reduce the "I could have".*

### 1. Two stories, one question

#### Story A: A dying man's wish for the moon

Years ago, I played *To the Moon* by Freebird Games.  

An old man named Johnny lies on his deathbed. His last wish is to "go to the moon." Two doctors enter his memories, traveling backward through time, trying to fulfill that wish. Layer by layer, they uncover the truth: as a child, Johnny met a girl named River at a carnival. They made a promise: *"If we ever get lost, meet me on the moon."*

But a traumatic accident – his brother's death – erased that memory. Drugs and grief buried the signal. River spent her entire life folding paper rabbits, building a house by the lighthouse, trying to wake him up. And Johnny's subconscious held onto one thing: *the moon.*

#### Story B: A snap, a time heist, and the cost of a second chance

*Avengers: Endgame* offers a different lens.  

After Thanos wipes out half of all life, the remaining heroes discover a way to travel back in time – not to erase their own regrets, but to steal the Infinity Stones before Thanos does, and bring everyone back.

But they quickly learn that changing the past doesn't change their present; it creates branching realities. Every jump introduces new variables. And in the end, Tony Stark faces the ultimate decision: use the Stones himself, knowing it will kill him, or let the universe stay broken. He chooses sacrifice. Steve Rogers, meanwhile, chooses a quiet life – staying in the past to finally dance with Peggy, the love he left behind.

Both stories ask the same question:

> *If you could go back to a critical moment, knowing what you know now, what would you choose? And what new consequences would you accept?*

### 2. The common dilemma: decisions are never purely rational

These narratives – one indie game, one blockbuster movie – share a hidden layer: **regret, emotion, and information noise corrupt our decision-making.**

- In *To the Moon*, Johnny's core signal (the promise) was buried under trauma and medication. He spent a lifetime acting on an impulse he couldn't explain. The question: how do we distinguish signal from noise when the noise is invisible?
- In *Endgame*, the heroes have future knowledge – a huge information advantage – yet they still face unforeseen branches. Dr. Strange sees 14,000,605 possible outcomes, but only one works. The lesson: knowing the future doesn't guarantee a perfect decision; it only reveals how many variables you cannot control.

In real life, we don't have time travel or memory-replay machines. But we do have something else: **the ability to audit our own decision logic before we commit.**

### 3. CronusCycle: a logic middleware for decision integrity

That idea became **CronusCycle** – an open-source decision audit middleware. Its companion, **Reborn**, lets you run a "pre-life audit" on important choices.

The core principle: **before you press the confirm button, see how your decision galaxy evolves.**

#### Galaxy Engine

I built a visualization engine that maps decision-making to astrophysics:

- **Stars** – core decision-makers (CEO, board)
- **Planets** – long-term executors, key influencers
- **Comets** – external advisors, temporary information
- **Meteors** – noise, one-off events
- **Black Holes** – high-risk unknowns
- **Gravitational Fields** – external forces (market, competitors, policies) that bend the decision orbit

Every major judgment leaves a trace – like the branching timelines in *Endgame*, or the layered memories in *To the Moon*.

#### Smart noise filtering

The hardest part of decision-making isn't lack of information – it's signal buried under noise.  

In *To the Moon*, River's paper rabbits: core signal or irrelevant noise? Johnny's amnesia: filtering or false deletion?  

CronusCycle uses lightweight ML models to identify high-frequency noise patterns. It doesn't make the decision for you. It clears the sky so you can see the stars clearly.

#### Explainable audit logs

Every decision path generates a plain-language audit log. Why did you choose A over B at this node? Which gravitational fields were pulling? Which meteors were filtered out?  

It's like Dr. Strange's view of 14 million timelines – but only for your own choices, and without the magic.

#### Time replay

You can drag a timeline and watch the decision evolve from initialization to the present. When did a gravitational field suddenly strengthen? Which planet deviated from orbit?  

It's a **"rebirth perspective"** – a rehearsal in the galaxy before the real move.

### 4. Why build this? (And why open source?)

People ask me: are you trying to eliminate bad decisions?

No. The real world will always have randomness and regret. But too much regret comes from *"I could have"* – I could have spotted that risk earlier. I could have seen my true motive. I could have grabbed the real signal before the noise drowned it.

- **For teams**: key talent loss, strategic drift – often not from lack of data, but from unacknowledged noise in the decision process.
- **For individuals**: career, marriage, entrepreneurship – once chosen, cannot be undone. But what if you could get a *simulation audit* before the leap?

Technology's human value is not to replace judgment. It's to make the trajectory of each judgment visible – so that regret, when it comes, is less often a *"I could have"*.

### 5. Current status and invitation

CronusCycle is still early. The documentation framework is in place, the core ideas are written down, and code is iterating. Reborn (the application layer) is in lab iteration.

But I believe a good technical product starts with its philosophy. That's why I'm sharing this now – before the code is perfect, before the stars are fully mapped.

If this resonates with you – if you've ever wondered how to filter social noise, enforce logic boundaries, or audit your own decision patterns – come take a look.

🔗 **GitHub**: [github.com/zerora-labs/cronus-cycle](https://github.com/zerora-labs/cronus-cycle)  
🌐 **Reborn**: [zerora.cn](https://zerora.cn)  
📫 **Contact**: bruce@zerora.cn

> *Not to eliminate regret, but to reduce the "I could have".*

------

*Image from the game To the Moon by Freebird Games. Used for non-commercial illustrative purposes.*

*This article is an English adaptation of a longer Chinese essay that references contemporary web series. For the full backstory (in Chinese), see [重生叙事与决策星系](重生叙事与决策星系.html).*



