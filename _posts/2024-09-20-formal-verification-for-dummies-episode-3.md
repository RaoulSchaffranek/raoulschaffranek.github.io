---
layout: post
title: "Formal Verification for Dummies, Episode 3: Proofs"
subtitle: Using a solidity debugger to explore time and space
tags: [Formal Verification, Symbolic Execution, Solidity, EVM]
comments: true
author: Raoul Schaffranek
---

In software development, achieving total confidence in code might sound like an unreachable goal. However, in formal verification, we aim to get as close to certainty as possible using proofs. These aren’t just any hand-wavy arguments—they’re mathematical demonstrations that a program behaves exactly as specified. But don’t worry, I’ll explain everything without diving into complex math. In this episode, we’ll break down what proofs are and how they’re used to verify software while keeping it simple and intuitive. Let’s explore how formal verification helps us approach near-perfect assurance in our code.

## Clarifying Terminology

Caution: the word "proof" is used in the blockchain ecosystem for quite some different things! You may have heard of **Merkle proofs** or **Zero-Knowledge proofs** - this is entirely unrelated to the formal verification proofs we’ll discuss here. So, try to clear your mind of any preconceptions you have about proofs in the blockchain space.

In formal verification, we use proofs to show that a program (or smart contract) conforms to a specification. At the heart of every proof is a claim—something like "This smart contract meets this specification." As discussed in Episodes 1 and 2, a specification is just a collection of requirements. To prove that a program conforms to a specification, we must show that it satisfies every individual requirement. So, really, we are proving many smaller claims, like "The smart contract satisfies this requirement."

It's important to note that a claim is not the same as a proof. A claim is simply a statement that may or may not be true. A proof is what we use to show that a claim is either true or false. If a claim has no proof attached to it yet, we don’t know whether it’s true—we call it an unproven claim or a proof obligation to emphasize that it's truth value is not yet determined.

## Mathematical Proof: a gold standard

In formal verification, proof is used in the strict mathematical sense. This is very different from the empirical proofs in sciences like experimental physics. What makes mathematical proofs unique is their eternity: once a mathematical proof is established, it cannot be overturned by new information. It stands forever. Contrast this with empirical proofs, which can be overturned by new evidence: Nobody has seen a unicorn, so we consider the claim "Unicorns exist" to be false. But if someone finds a unicorn one day, that claim would be proven true. This is not the case with mathematical proofs. The defining characteristic of a mathematical proof is that it can be reliably reproduced and counter-checked by everyone and we would always arrive at the same conclusion! 

## Mechanical Proofs: keeping us honest

Of course, humans make mistakes, and mathematicians are no exception. Sometimes, we think we've found a proof but later realize there was an error. Does that conflict with the idea of a proof being eternal? Not at all—it simply means there never was a valid proof to begin with.

In software verification, the complexity of proofs increases since claims can involve hundreds of variables, and proofs can span ten thousand steps. This has nothing to do with the friendly two-column proofs you might remember from high school geometry. This brutal, unforgiving work requires a level of precision that humans can't always provide. To minimize human error, we therefore rely on computers to find and check these proofs for us. A proof checker ensures that each proof step is justified by an eligible rule, providing confidence in the proof’s correctness. We'll cover this in more detail later when we learn about proof systems.

## Correctness: A relative concept

You might hear people say, "We have proven the correctness of the program/the smart contract." This can be misleading because "correctness" is not absolute. What they really mean is that the program conforms to a particular specification. If the specification is incomplete, bugs can still exist in the code—even if it's formally verified. Proofs are absolute, but correctness is always relative to the specification. That's precisely the reason why 100% certainty of a program being bug-free is not archivable. Maybe our specification is just incomplete. Determining when a specification is complete is a philosophical question, but the answer that most formal verification engineers will give is simply "never".

Interestingly, it is much easier to show that a program is incorrect—i.e., that it doesn’t conform to its specification. We only need a single example where the program fails to meet a requirement. However, proving correctness requires us to show that every possible program execution meets every single requirement. Typically, there is an infinite of potential executions to consider.

## Stuck Proofs: Disguised Progress

When working on a proof,  you might get stuck, which simply means you don't know which proof step to take next in order to progress toward the final goal. This is also true for automatic proof-searching tools. This can feel frustrating for beginners, but it’s not wasted effort. Even a stuck proof can be valuable. We only say we have proven a given requirement when we have proven it for **all** execution paths. When we've only proved for half of the paths, that's still incredibly valuable and usually a much stronger correctness guarantee than what any unit test or fuzz test can offer us.

## Proof Systems: The Rules of the Game

Proofs are often done with pen - and paper and they often skip "obvious" proof steps. Skipping steps are performed on all educational levels, from primary school to scientific math papers. This sometimes leaves the impression that the granularity or the steps we're allowed to take are somewhat arbitrary. A university professor is allowed to take larger steps than a first-semester. Of course, this is not the case! The rules are the same for everyone. And they're very clearly defined. When a math professor skips steps, that's usually because he thinks that the intermediate steps are obvious, and spelling them out would distract the audience from the more intricate bits of the proof. And yes, sometimes the skipped steps are actually invalid!

So, how many rules are there? Surprisingly, there is just a dozen of rules that we can and must follow when taking proof steps called "axioms" and "inference rules". Axioms constitute the valid starting points for proofs. And inference rules describe exactly which steps we're allowed to take. That is, every step we take must be justified by such an inference rule. These rules govern the eligible steps of proof. If one of the steps is not justified by a rule, then we don't have a proof! It's simple as that! The axioms and inference rules that underlie most of today's mathematics are called [Zermelo-Fraenkel set theory}(https://en.wikipedia.org/wiki/Zermelo%E2%80%93Fraenkel_set_theory).

Actually, there are different proof systems used in different branches of mathematics and computer science! And to make it all worse, a claim that might be proven in one proof system, might actually be false in a different proof system! After all, when I said proofs are absolute, I lied to you! Proofs are relative to the proof systems they've been conducted in. You don't have to worry about this too much - but there are a couple of critical consequences that we must consider when doing formal verification: we should know which proof systems we're using, and we better make sure the allowed proof rules don't contradict each other. Why? Because it would mean that for any claim we can prove it and disprove it! So basically, we can show that a program conforms to the specification or not, depending on our mood. Clearly, this is not what we want!

## Kontrol’s Proof System

[Kontrol}(https://kontrol.runtimeverification.com/), the formal verification tool for Ethereum developed by Runtime Verification, uses a specific proof system known as reachability logic and matching logic. These systems were designed specifically to prove properties about programs. You absolutely don't need to understand these logics to use Kontrol. In most cases, it is sufficient to know that such a proof system exists at the core of Kontrol.

## Other Arguments

Mathematical, machine-checked proofs are the strongest form of argument that we can make to show that a program conforms to a specification. But the bar for these proofs is high and not easily achievable. That's why I want to devote the last part of this article to other forms of arguments.

Remember, showing that a program is incorrect is much easier than showing that it is correct. So, it's not surprising that there are many tools that can help us find bugs, but not many that can help us prove correctness. In the Ethereum ecosystem, there's a wide range of tools, such as unit testing frameworks like Hardhat, fuzzers like Echidna and Foundry, and symbolic execution tools like the Certora Prover, Halmos and HEVM.

What all these tools share is that they can be used to show that a program **does not** conform to a specification, but they generally cannot be used to prove that it **does**. Now, Certora, Halmos, and HEVM build really strong arguments, performing an extensive bug search, and that's why they're often referred to as "formal verification" tools. The bar that we set for formal verification in this article, however, is pedantically high - namely, that the tool produces mathematical, machine-checked proofs. And that's not the case for these tools, mainly due to the following reasons:

- As we have seen, valid proofs consist of a series of proof steps, each justified by an eligible proof rule. Bounded symbolic execution tools typically lack such proof systems and instead follow some ad-hoc rules that are not formally laid out. Consequently, it's not possible to re-produce or counter-check the proofs externally.
- We require that our proofs are exhaustive, which means they cover all potential program executions, but bounded symbolic model-checking tools generally struggle with unbounded loops and dynamic data structures, such as arrays and strings. They perform an extensive but not exhaustive search. This basically means they can miss bugs not only due to an incomplete specification but also due to incomplete bug search - and that's not acceptable according to the high bars we set for mathematical proofs in this article.

This is not to downplay the value of these tools—they're all S-tire security tools! However, it's important to remember this information when comparing these tools. Way too often, people compare security tools only based on their execution speed and neglect the correctness assurance level they can provide. 

## Summary

In this episode, we explored the role of proofs in formal verification, emphasizing that proofs help us demonstrate that a program conforms to a given specification. We clarified the distinction between mathematical proofs and empirical proofs. We also discussed how **mechanical proof checkers** help reduce human error in verifying complex software.

The episode further highlighted the relative nature of **correctness**, meaning a program conforms to a specification, and explained how proving incorrectness is often easier than proving correctness. We also covered the challenges of **stuck proofs** and how they still provide valuable insights. We briefly touched on **proof systems** - the rules that govern eligible proofs and discussed how formal verification relates to other bug-finding tools.