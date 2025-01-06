---
layout: post
title: "Formal Verification for Dummies, Episode 2: Invariants"
subtitle: Using a solidity debugger to explore time and space
tags: [Formal Verification, Symbolic Execution, Solidity, EVM]
comments: true
author: Raoul Schaffranek
---

Hello again! Today, we’re tackling a super important concept in software testing and formal verification: invariants. If you’ve worked in the Ethereum ecosystem, you’ve probably heard people throw this term around as a catch-all for software requirements, but what does it really mean? In this episode, we’re breaking down the difference between requirements and invariants and why they matter when building secure smart contracts.

Let’s start with the requirements. In the [first episode](TODO), we discussed the purpose of specifications and what makes a good one. Now, we’ll focus on their content. Essentially, a specification is a collection of software requirements. For a piece of software to conform to a specification, it must fulfill every single requirement. Let’s look at some examples using fungible tokens:

- R1: "Assume Alice has X tokens, and Bob has Y tokens. After transferring Z tokens from Alice to Bob, Alice MUST have X - Z tokens, and Bob MUST have Y + Z tokens."
- R2: "For the contract's lifetime, the sum of all balances MUST always equal the total supply of tokens."
- R3: "Assume Alice has X tokens. After minting Y tokens to Alice, her new balance MUST be X + Y tokens."
- R4: "Assume Alice has X tokens. After burning Y tokens from Alice, her new balance MUST be X - Y tokens."
R5: "For the contract's lifetime, the number of minted tokens minus the number of burned tokens MUST equal the total supply."
- R6: "When the contract is paused, the contract MUST revert on all transactions."
- R7: "When the contract is paused, a privileged admin MUST always be able to unpause it."
- R8: "The token has 18 decimals."

*Tip: Always enumerate requirements so they can be referenced.*

## Breaking Down Requirements

Let’s take a closer look at R1. To satisfy this requirement, an implementation candidate must update the balances correctly for all possible inputs and in all possible states. Here, Alice, Bob, and Z are the input variables. Alice and Bob are placeholders for arbitrary addresses, and Z represents the transferred amount. The state variables X and Y represent Alice’s and Bob’s token balances before the transfer. It’s insufficient to meet this requirement for just a few specific cases. It must hold true for every possible combination of balances, addresses, and transferred amounts.
This is crucial for security—if even one input or state combination doesn’t satisfy the requirement, the implementation doesn’t conform to the specification. It might sound strict, but this is how it should be. Most security exploits happen because the software behaves incorrectly under some rare or unexpected set of inputs.

Let's examine some weird edge cases to understand the requirements and how we can improve them for precision.
For example, what happens if Alice tries to transfer more tokens than she has? In other words, what if Z > X? We’d expect the transaction to revert, but our original requirement doesn’t cover that. To fix this, we can refine it by making a case distinction.

- R1a: "Assume Alice has X tokens, and Bob has Y tokens. Further, assume Z <= X. After transferring Z tokens from Alice to Bob, Alice MUST have X - Z tokens, and Bob MUST have Y + Z tokens."
- R1b: "Assume Alice has X tokens, and Bob has Y tokens. Further, assume Z > X. Attempting to transfer Z tokens from Alice to Bob MUST revert."

Let’s consider another interesting edge case: what happens if Alice tries to transfer tokens to herself? To explore this, we mentally replace “Bob” with “Alice” in the requirement:

- "Assume Alice has X tokens, and Alice has Y tokens. Further, assume Z <= X. After transferring Z tokens from Alice to Alice, Alice MUST have X - Z tokens, and Alice MUST have X + Z tokens."

This is clearly self-contradictory—Alice’s balance can’t both increase and decrease at the same time. Let’s refine the requirement again:

- R1a: "Assume Alice and Bob are different. Assume Alice has X tokens and Bob has Y tokens. Further, assume Z <= X. After transferring Z tokens from Alice to Bob, Alice MUST have X - Z tokens, and Bob MUST have Y + Z tokens."
- R1b: "Assume Alice has X tokens. Further assume Z <= X. After transferring Z tokens from Alice to herself, Alice’s balance MUST remain unchanged."
- R1c: "Assume Alice has X tokens, and Bob has Y tokens. Further, assume Z > X. Attempting to transfer Z tokens from Alice to Bob MUST revert."

This process of refining requirements is part of requirements engineering, which is essential for developing clear, effective specifications. If you don’t explicitly write down assumptions—like Alice and Bob being different—then those assumptions only exist in your head. Your colleague might not share them, leading to miscommunication or even security vulnerabilities.

If you want to practice requirements engineering, you can examine the requirements above, identify unclear edge cases and contradictions, consider new requirements for fungible tokens, or pick another standard, such as non-fungible tokens or tokenized vaults. Writing clear specifications is a skill that can be practiced, and there is essentially not much you can do wrong - you write down your assumptions and expectations. If you later find out that one assumption is not practical, you go back and refine it.

## Understanding Invariants

After briefly discussing requirements, let’s finally discuss invariants. Requirements can be roughly classified into those describing what **should** and **should not** change. The former are often called "correctness properties," while the latter are called invariants. From our earlier examples, R2, R5, and R8 are invariants.

Invariants can be as simple as R8: "The token has 18 decimals." This is a constant that shouldn’t change over the contract's lifetime. However, invariants can also be more dynamic, like R2, which states that the sum of all balances must always equal the total supply. Consider the case when this invariant does not hold. It would mean some user owns tokens that are not accounted for in the total supply or a user lacks access to tokens he rightfully owns. Both scenarios are critical security issues.

Notice that R2 allows the individual balances and the total supply to change; they're not constant, but their relationship is fixed.  Most interesting invariants establish relationships between state variables that should always hold.

Now, what do we mean by "always"? It’s not absolute—there are brief moments, such as when tokens are minted or burned, where the invariant might not hold. After all, when minting, we must increase the total supply and the recipient's balance after one another, so there is a brief moment when only one of the variables has been updated, and their relationship is temporarily broken. This is unavoidable and indeed acceptable. But what’s important is that the invariant holds:

- At the start of the contract (when it’s freshly deployed).
- After every external and internal transaction.
- Crucially, right before the contract makes any external call.

This last point is often overlooked but is critical. Forgetting to check this last point leads to reentrancy bugs. When an external call is made, we expose our contract to the outside world, so it must be in a consistent state where all invariants are intact. Failing to check this box has caused billion-dollar losses.

## Summary

In this episode, we explored the difference between requirements and invariants. We learned that:
Requirements define what a software must do under all possible inputs and states. Refining these requirements cases is crucial for clarity and security.

Invariants specify what must never change, even as the system evolves. They are essential for ensuring a contract's consistent behavior, especially in scenarios involving complex interactions or external calls.

We also saw how refining requirements and making assumptions explicit helps avoid contradictions and security issues. Clear, well-defined specifications are key to building robust and secure software.

I should note that this episode only covered contract invariants. There is a related concept called "loop invariants", that I'll save for a later episode.