---
layout: post
title: EthBelgrade - Debugging meets Formal Methods
subtitle: Smart contract debugging and formal verification
tags: [Conference, Talk, Formal Verification, Symbolic Execution, Debugging, Solidity, EVM]
comments: true
author: Raoul Schaffranek
cover-img: /assets/img/eth-belgrade-2024/eth-belgrade.jpg
---

### Demystifying Formal Verification: Tools and Techniques for Smarter Smart Contract Development

In a recent talk at EthBelgrade, I had the chance to dive into formal verification and introduce tools that make this advanced approach more accessible to developers and security researchers. Formal verification has traditionally been the domain of large-scale projects like Ethereum's deposit contract, Uniswap, and Optimism. However, we're working to bridge the gap for smaller teams and independent auditors by simplifying its application.

#### Why Formal Verification Matters

Formal verification takes confidence in smart contracts to the next level by mathematically proving the correctness of code. While fuzzing can expose vulnerabilities by generating random inputs, it doesn't guarantee the absence of bugs. Symbolic testing, a flavor of formal verification, provides either:
- A **counterexample**, indicating a bug, or  
- A **proof** that no such counterexample exists.

This method eliminates the uncertainty inherent in fuzzing, offering peace of mind that critical vulnerabilities won’t go undetected.

#### Introducing Simbolik: A Symbolic Solidity Debugger

We developed **Simbolik**, a hybrid tool combining traditional debugging with symbolic execution. Here’s why it’s a game-changer:
- **Debugger Features**: Set breakpoints, step through code, and inspect memory, stack, and storage.  
- **Symbolic Execution Mode**: Visualize abstract state transitions to systematically explore all potential paths, uncovering vulnerabilities hidden in edge cases.  
- **Browser-Based Demo**: Try it at [simbolik.runtimeverification.com](https://simbolik.runtimeverification.com) without installing anything.

#### Symbolic Testing vs. Fuzzing

Fuzzing works by throwing random inputs at tests, while symbolic testing operates on abstract states, replacing concrete values with symbolic variables. This enables it to:
- Explore infinite state spaces using symbolic reasoning.
- Provide rigorous proofs or pinpoint exact failure scenarios.

#### The Roadmap

We’re just getting started. Upcoming features include:
- **On-Chain Debugging**: Debug transactions directly from Ethereum mainnet.  
- **Enhanced Visualizations**: Graphical state exploration to improve usability.  
- **Full EVM State Inspection**: A deeper dive into the Ethereum Virtual Machine.  
- **Integration with Foundry**: Support for Foundry cheat codes and seamless debugging of Foundry tests.  

#### Formal Verification: When and Why?

While formal verification is resource-intensive, it’s invaluable for mission-critical smart contracts. Tools like **Kontrol** simplify the process by allowing Foundry test suites to double as formal specifications. This streamlines adoption and ensures comprehensive testing.

For non-critical projects, fuzzing may suffice. However, for high-stakes systems, incorporating formal verification into CI/CD pipelines provides unparalleled security and confidence.

---

Formal verification and symbolic debugging aren't just for the big players anymore. Tools like Simbolik and Kontrol are paving the way for broader adoption, making these techniques accessible and practical for all Solidity developers.

**Explore Simbolik:** [Try the demo](https://simbolik.runtimeverification.com)  
**Learn more about Kontrol:** [Visit the documentation](https://kontrol.runtimeverification.com/)

We’re eager to hear your feedback and collaborate to make smart contract development safer and more reliable. Let’s build better contracts together!

<iframe width="560" height="315" src="https://www.youtube.com/embed/6Kl4UvWjO8Y?si=AypfaZga3ReWD8z9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>