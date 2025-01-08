---
layout: post
title: "DeFi Security Summit - Solidity under the hood"
subtitle: Using Simbolik to understand compiler internals
tags: [Conference, Talk, Debugging, Solidity, EVM, Compiler]
comments: true
author: Raoul Schaffranek
---

## Inside the Solidity Compiler: A Peek Into Boilerplate Code & Variable Allocation

I recently had the opportunity to present a workshop on Solidity compiler internals at the DeFi Security Summit. Although the session wasn’t recorded, you can still explore the slide deck [here](https://drive.google.com/file/d/1769PkfOYA0kfjFAARIFnL5HKaxE1zi76/view). The main goal of this talk was to educate Solidity developers and security researchers on how to use **Simbolik** — the Solidity debugger — to better understand the compiler’s inner workings. To this end, I worked with two major examples:

- **Boilerplate Code Generation** \
  Every Solidity contract includes auto-generated boilerplate code to validate inputs and dispatch function calls. By examining this code, you gain deeper insight into how the compiler handles control flow before any of your own logic executes.
- **Variable Allocation** \
  We also explored how the compiler allocates variables in different data locations (storage, memory, and calldata) and for various data types. A solid understanding of allocation strategy helps with gas optimization and security considerations.

If you’re curious about these topics — or want to see how Simbolik can reveal what’s going on under the hood—check out the slides. Feel free to reach out if you have any questions or want to continue the discussion!
