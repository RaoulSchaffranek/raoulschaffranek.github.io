---
layout: post
title: "Formal Verification for Dummies, Episode 1: Specifications"
subtitle: Using a solidity debugger to explore time and space
tags: [Formal Verification, Symbolic Execution, Solidity, EVM]
comments: true
author: Raoul Schaffranek
cover-img: /assets/img/fv-for-dummies/fv-for-dummies-1.jpg
---

Hey everyone! Welcome to the first episode of my new series, "Formal Verification for Dummies." My goal here is to explain complicated topics in simple terms to help others and improve my ability to break things down. I’m not sure how many episodes I’ll do or how often I’ll post—this is just for fun, and when the fun stops, I’ll stop posting! Today, we’re starting with a key concept: **specifications**.

So, what’s the deal with formal verification? In short, it’s about making sure a program (or smart contract) does precisely what it’s supposed to do. But here’s the catch: if you ask 10 developers what a program should do, you’ll probably get 11 different answers! That’s a problem, right? One might think a feature works perfectly, while another sees a huge security issue. This even leads to what we call “escalation wars,” where security researchers argue over their expectations. So, how do we avoid all that confusion? The answer is simple: we must agree on what the program should do and write it down. That’s where specifications come in.

Now, what makes a **good** specification? There are a few things: it needs to be **accessible**, **complete**, **consistent**, and **verifiable**. Let me break it down.

- **Accessibility** means everyone who needs to use the specification can understand it. A common mistake is writing specs that are so technical that only the most experienced developers get them, leaving the new folks confused.
- **Completeness** means your spec should cover all the expected behaviors—both what you want the program to do and what you don’t want it to do. Of course, perfection isn’t realistic. We often find gaps in the spec as we go, and that’s fine! Refining the details as you work is normal, and it’s way easier (and cheaper) to fix things at the spec level than during implementation or maintenance. Specifications are living documents!
- **Consistency** is pretty straightforward: the spec shouldn’t contradict itself. Conflicting expectations are a recipe for disagreements where both sides can argue they’re “right” based on the same spec. When this happens, catching and sorting out these inconsistencies is essential as part of the regular process.
- **Verifiabe** means the spec should be detailed enough that we can objectively judge if the program meets it. Specs written in plain language are a great starting point because they’re easy to understand, but natural language can be vague or overly verbose. That’s why some specs also include mathematical descriptions—they’re clearer but still rely on human judgment. The most precise form of specification is an **executable** specification, which means the computer can automatically verify it for you. These specifications can be written in special-purpose verification languages or directly in the implementation language of the program being analyzed. For instance, the K language is a powerful verification language known for its expressiveness, though it requires a bit of experience to use effectively. More commonly, these days, we write our specs directly in Solidity in the form of property tests. If you’ve ever worked with a unit testing framework, you’ve already encountered executable specifications in action. The difference between testing and verification lies in how the tests are executed. Running tests with a tool like Foundry is considered testing, where the goal is to break the code through brute force. On the other hand, running those same tests with a tool like Kontrol is considered verification. Kontrol approaches your tests with mathematical rigor, exploring every possible program path to ensure the code behaves correctly in all scenarios, not just a subset.

In the world of formal verification, we’re mainly focused on **executable specifications**. Still, I can’t stress enough how important it is to have clear, accessible, and well-written natural language specs as a foundation. They’re the bridge that helps everyone get on the same page before diving into the technical details.

If you have any questions about formal verification, please post them in the comments, and I’ll attempt them in future posts.