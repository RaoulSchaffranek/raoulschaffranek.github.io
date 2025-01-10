---
layout: post
title: EthBucharest - Using a solidity debugger to explore time and space
subtitle: About time
tags: [Conference, Talk, Symbolic Execution, Debugging, Solidity, EVM]
comments: true
author: Raoul Schaffranek
cover-img: /assets/img/eth-bucharest-2024/eth-bucharest.jpg
---

### Exploring the Future of Smart Contract Debugging with Symbolic Execution

At EthBucharest, I had the pleasure of introducing a new tool aimed at making formal methods more accessible for Ethereum developers and security researchers. Building on feedback that formal methods often feel too complex, our team at Runtime Verification launched **Simbolik**, a state-of-the-art Solidity debugger designed to simplify reasoning about smart contracts while addressing vulnerabilities in their transaction histories.

#### Key Highlights from the Presentation:

1. **Abstracting State Space**  
   Smart contracts operate within the Ethereum Virtual Machine (EVM), a vast state machine. Simbolik uses **symbolic execution** to collapse the infinite state space of possible transaction sequences into manageable, abstract representations. This enables developers to reason about their code and spot vulnerabilities with ease.

2. **Transaction-Level Debugging**  
   Our debugger breaks down transactions at both the Solidity and EVM levels. Developers can inspect Solidity variables, memory, stack, and even step through bytecode—ideal for understanding intricate bugs and optimizing gas usage.

3. **Time and Space Navigation**  
   Borrowing the concept of "time travel debugging," Simbolik allows not only backward execution but also exploration of alternative code paths. For instance, you can easily switch between branches of an `if` statement to see how different conditions impact the execution.

4. **Accessible and Open-Source**  
   Simbolik is browser-based—no installation required—and will soon be open-sourced to foster community-driven improvements. It integrates seamlessly with Visual Studio Code and other IDEs via the Debug Adapter Protocol.

5. **Future Plans**  
   Upcoming features include decoding Solidity storage variables, Foundry integration for stepping through tests, and potential support for mainnet transaction debugging. Imagine copying a transaction hash from Etherscan and replaying it directly in your browser!

This is just the beginning for Simbolik. We’re building for the community, and your feedback is invaluable. Check out the public demo on our website, and let us know what features you’d like to see!

**Watch the full presentation here:**

<iframe width="560" height="315" src="https://www.youtube.com/embed/PIS3v9LPPdU?si=ZHKxhOXNsxlnUl59" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Let’s make formal methods accessible to everyone—one debug session at a time.
