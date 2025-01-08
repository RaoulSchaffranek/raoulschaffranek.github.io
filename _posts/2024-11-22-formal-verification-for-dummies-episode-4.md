---
layout: post
title: "Formal Verification for Dummies, Episode 4: Scaling"
subtitle: Using a solidity debugger to explore time and space
tags: [Formal Verification, Symbolic Execution, Solidity, EVM]
comments: true
author: Raoul Schaffranek
cover-img: /assets/img/fv-for-dummies/fv-for-dummies-4.jpg
---

*It’s been a while since my last post in this series. In the meantime, I’ve published two in-depth technical articles on verifying loop invariants for [Runtime Verification](runtimeverification.com). Read them here: [Part 1](https://runtimeverification.com/blog/formally-verifying-loops-part-1) and [Part 2](https://runtimeverification.com/blog/formally-verifying-loops-part-2)*

*I’m excited to be back with this new post! Today’s article is a bit different — it’s an opinion piece.*

**Can formal verification keep up with the growing complexity of on-chain code?**

This question was recently discussed on a panel, Demystifying Smart Contract Security: Facts & Fallacies, at DevCon Thailand ([watch the recording](https://www.youtube.com/watch?v=eltgxBe-OpM)). Panelists Harikrishnan Mulackal, Josselin Feist, Matthias Egli, Mehdi Zerouali, and Mooly Sagiv, moderated by Rajeev, shared their insights. Harikrishnan, the CEO and co-founder of Spearbit and Cantina, made a bold claim: "Formal verification fundamentally cannot scale by design,"  adding that "the complexity of DeFi grows linearly, while the complexity of formal verification grows exponentially." The spicy discussion starts at [32:26](https://youtu.be/eltgxBe-OpM?si=3qHumwHXYY7DSrIt&t=2366)

Hot takes like this are fantastic discussion starters, so I couldn’t resist unpacking the claim and sharing my perspective.

## Complexity Is Everyone’s Problem

First off, I have to disagree with the idea that the complexity of DeFi protocols grows only linearly. If anything, it’s growing faster than that. Take Uniswap: V4 isn’t just four times as complex as V1 — it’s likely an order of magnitude more complicated, no matter how you measure it. Non-linear growth is the real challenge for all security techniques, not just formal verification.

This increase in complexity stretches the limits of audits, fuzzing, and testing and any other security technique. Audits require more time, deeper analysis, and higher costs, while fuzzing and testing campaigns focus on broader coverage (more lines of code) without significantly improving depth (exploration of the state space).

And let’s not forget the sheer size of those state spaces: a single uint256 variable can hold 2^256 possible values—compare that to the number of atoms in the observable universe: 10^80. Fuzzing offers a tiny fraction of state space coverage, close to 0%. Formal verification, in comparison, can achieve complete coverage under the right conditions.

## Formal Verification Enables Innovation

Formal verification often acts as a catalyst for innovation rather than a bottleneck. Some of the most complex DeFi protocols and infrastructure projects today—I'm thinking of Lido, Aave, Morpho, Optimism, and zkVMs—rely heavily on formal verification to ensure their security. These projects prove that formal verification scales alongside complexity. Harikrishnan acknowledged this during the panel, so we’re aligned here.

Looking forward, it’s worth noting that formal verification is already being used successfully in way more complex systems outside DeFi, proving that its potential scales beyond today’s challenges.

It’s equally important to remember that innovation in DeFi doesn’t always mean increased complexity. Some of the most transformative ideas—like NFTs, DEXs, or Ethereum’s shift from PoW to PoS—succeeded largely because of their on-chain simplicity.

Consider Ethereum’s deposit contract for the PoS transition: formally verified by Runtime Verification. The stakes couldn’t have been higher—failure would have jeopardized Ethereum’s entire transition. Transformative changes like Ethereum’s PoS upgrade or other invasive protocol updates would seem downright reckless without rigorous security measures. Formal verification is crucial to that equation, alongside audits, fuzzing, and static analysis.

## Evolving Accessibility and Misconceptions

One of the things that makes me most optimistic about the role of FV in blockchain security is the pace at which our tools evolve. Over the past year, tools have improved significantly, making it easier than ever for teams to adopt these techniques. While it’s not exactly easy yet, the progress is encouraging. These improvements give me hope that formal verification will scale alongside the protocols it aims to protect. In fact, I'd argue the situation is improving and not worsening.

It’s important to recognize that formal verification is an umbrella term encompassing a variety of tools and techniques. Some prioritize speed, like the Certora Prover and Halmos, while others, such as Kontrol, focus specifically on tackling growing codebases with mechanisms to overcome stuck states or timeouts.

Choosing the right tool for your use case is essential—different tools have different strengths.

## Conclusion

Formal verification is not a silver bullet but a powerful collection of tools and techniques that continue to evolve and adapt alongside the DeFi ecosystem. By embracing formal verification alongside other security practices, we can build systems that are not only more secure but also inspire greater confidence in the blockchain space. The future of DeFi depends on scaling security as effectively as we scale innovation—and formal verification is an indispensable part of that equation.

As DeFi grows more complex, no single security approach will be enough to ensure safety. Formal verification has challenges, but it also offers unmatched benefits. It’s not about formal verification vs. other methods—it’s about leveraging the strengths of each to create a comprehensive security strategy.

Finally, I think the biggest scaling challenge for formal methods is not adapting to increasing code sizes but attracting more talent to fulfill the demand ahead of us.