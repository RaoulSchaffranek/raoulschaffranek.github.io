---
layout: post
title: SecureFi - Formal Verification Panel
subtitle: with Kostas Ferles, Mooly Sagiv, Alexander Hicks and Julian Sutherland
tags: [Conference, Panel, Formal Verification, Symbolic Execution]
comments: true
author: Raoul Schaffranek
cover-img: /assets/img/securefi-2024/securefi-panel.jpg
---

### Breaking Down Barriers: Formal Verification in the Blockchain Space

I was honored to moderate a recent panel at the SecureFi conference, featuring Kostas Ferles (Veridise), Mooly Sagiv (Certora), Alexander Hicks (Ethereum Foundation), and Julian Sutherland (Nethermind). These experts came together to explore one of the most critical questions in smart contract security: how can formal methods (FM) achieve broader awareness and adoption in the blockchain ecosystem? Here's my summary of the rich and multi-faceted discussion. You can find the full recording at the end of this post.


### Why Use Formal Methods?

The panel began by addressing the core question: *What problems are formal methods solving in blockchain?*

- **Trust in Code**: Formal verification offers a unique way to establish confidence in the correctness of code, particularly important in trustless systems like blockchain.
- **High-Complexity Systems**: ZK circuits, cryptographic verifiers, and optimized assembly code are examples of where formal methods shine, as they reduce human error and enhance trust in complex computations.
- **Beyond Implementation**: Formal methods validate not only implementation correctness but also protocol designs, ensuring specifications align with intended functionality.

### Do We Always Need Formal Methods?

A common concern is when and whether formal verification is worth the investment.

- **"Use Everything"**: The unanimous advice was to adopt as many tools as possible—manual audits, fuzzing, static analysis, and formal verification—tailored to the budget and context.
- **Limited Budgets**: For time-boxed engagements, panelists emphasized starting early with lightweight specs. Even "bad specifications" or simple properties can uncover meaningful issues. 
- **Project Types**: Protocols handling large funds, mathematical complexity, or ZK systems benefit most from formal methods. Conversely, simpler contracts might not need exhaustive formal verification.

### What Makes a Good Specification?

The panelists dug deep into the challenges of crafting useful specifications.

- **Completeness Is a Myth**: Specifications will always have limitations. The key is to identify the most critical properties to verify.
- **Collaboration Is Key**:
  - Developers and security researchers should co-create specs, combining protocol knowledge with formal methods expertise.
  - Formal methods engineers should formalize ideas and filter ambiguities, ensuring specifications are rigorous and meaningful.
- **Mindset Matters**: Writing good specifications requires curiosity, a "negative mindset" to anticipate what can go wrong, and clarity in expressing assumptions.

### Who Can Write Specifications?

A lively debate emerged over whether PhD-level expertise is essential for formal methods, with differing perspectives on the panel. However, I feel that Julian Sutherland was misunderstood in this discussion, and I don't think I did a good job moderating this part of the debate. Julian did not claim that you need a PhD to write specifications. Rather, his point was that even experts who have been writing specifications for years—sometimes with advanced mathematical or formal training—often make mistakes during the process. These mistakes can lead to severe damage, especially in high-stakes contexts like blockchain protocols.

This nuance is important because it highlights the inherent challenges of specification writing. It’s not just about whether someone has formal education or expertise—it’s about the difficulty of accurately capturing complex invariants and edge cases in a way that aligns underlying business logic. Julian’s perspective underscores the need for rigorous review processes, collaboration, and tools to support those writing specifications, regardless of their background.

The discussion also touched on broader views:

- The Case for Experts: Writing accurate, high-quality specifications often requires advanced skills in logic and mathematics, which experts develop over years of study and practice. For systems of high complexity, this expertise can be indispensable.
- The Case Against Exclusivity: Many non-experts, including developers and security researchers, have demonstrated the ability to write effective specifications, especially with the help of accessible tools and good documentation.

Ultimately, the panel agreed that empowering more people to contribute to specification writing is critical, whether they are seasoned experts or developers just starting out. By improving tools, training, and collaboration, the goal is to make formal methods an inclusive practice while mitigating the risks inherent in specification writing errors.

### Lowering Barriers to Entry

Panelists agreed that increasing awareness and usability are crucial to scaling formal methods adoption.

- **Tool Accessibility**: 
  - Remove jargon from tools and documentation to reduce the intimidation factor.
  - Integrate formal methods into familiar developer environments, like Foundry.
- **Contests and Incentives**:
  - Public verification contests (e.g., EulerDAO’s initiatives) have proven successful in onboarding new users and incentivizing participation.
  - Gamifying specification-writing or rewarding continuous contributions (e.g., through CI pipelines) could further increase engagement.
- **Education**: Workshops, community courses, and even "crypto zombies" for formal verification can make learning engaging and practical.

### The Future of Formal Methods

The panel concluded with exciting visions for formal verification in blockchain:

- **ZK-Integrated Formal Methods**: Emerging frameworks, like Nethermind's use of Lean 4 to verify ZK circuits, hint at a future where verification and zero-knowledge proofs combine seamlessly.
- **On-Chain Verification**: Reward systems could incentivize creating reusable, on-chain formal proofs, enabling trustless cross-contract calls with verified correctness.

### Key Takeaways for Developers

1. **Start Small**: Write simple specs early; even lightweight properties can have significant impact.
2. **Experiment with Tools**: Explore accessible tools like Foundry, Certora and Clear for both fuzzing and formal verification.
3. **Collaborate and Learn**: Partner with formal verification experts and leverage contests, workshops, or open-source communities for guidance.
4. **Think Long-Term**: While formal methods can be time-intensive, their benefits compound over time, particularly in high-stakes systems.

Formal methods may be challenging, but their value in securing blockchain systems is undeniable. By building better tools, improving education, and fostering collaboration, the blockchain space is poised to make formal verification a standard part of the development lifecycle.

<iframe width="560" height="315" src="https://www.youtube.com/embed/TIu_AFkPd8c?si=QUpSpqFLl4Kw6Y1V" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>