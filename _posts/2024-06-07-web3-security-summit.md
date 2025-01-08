---
layout: post
title: Web3 Security Summit - Fuzzing vs. Formal Verification Panel
subtitle: "TL;DR: Do both"
tags: [Conference, Talk, Formal Verification, Symbolic Execution, Debugging, Solidity, EVM]
comments: true
author: Raoul Schaffranek
---

### Formal Verification vs Fuzzing: Key Takeaways from the Panel

At a recent panel discussion, Mooly Sagiv (Certora), Josselin Feist (Trail of Bits), Josef Gattermayer (Ackee) and me came together to compare **formal verification** and **fuzzing** — two powerful approaches to enhancing smart contract security. Here’s my summary of the key insights shared during the lively debate. You can find the full recording at the end of the post.

---

### **1. Definitions and Strengths**
- **Fuzzing**: A more hands-on, engineering-driven approach that generates inputs to test the contract’s behavior. Guided fuzzers like those in Foundry or Wake allow developers to direct the exploration of state spaces, while black-box fuzzers randomly test for vulnerabilities.
  - **Strengths**: 
    - Quick to set up and execute.
    - Highly effective for detecting arithmetic bugs, rounding issues, or unexpected edge cases.
    - Excellent for testing against real-world integrations using mainnet forks.
  - **Challenges**:
    - Limited by the coverage of input generation.
    - May struggle to identify deeper logic bugs or prove correctness.

- **Formal Verification**: A mathematically rigorous method that uses provers to either:
  1. Find counterexamples to the specified properties.
  2. Prove that no such counterexample exists.
  - **Strengths**:
    - Provides proofs of correctness, giving unmatched confidence.
    - Systematically explores state spaces, including symbolic paths that fuzzers might miss.
    - Reuses property tests written in Solidity, as demonstrated by tools like Kontrol.
  - **Challenges**:
    - Requires formal specifications, which can be difficult to define.
    - Computationally intensive, with a learning curve for non-experts.

---

### **2. When to Use Which?**
The panelists agreed that **both approaches are complementary**, and ideally, both should be used. However, they offered practical guidance for choosing between them:
- **Limited Budget or Time**: Start with fuzzing. It’s faster to set up, requires less expertise, and provides good initial coverage.
- **Critical Properties**: For invariants where absolute correctness is essential (e.g., preventing fund loss), formal verification offers unmatched guarantees.
- **Iterative Development**:
  - Begin with fuzzing to catch low-hanging bugs.
  - Once the codebase stabilizes and invariants are well-defined, apply formal verification for higher assurance.

---

### **3. The Overlap and Convergence**
Fuzzing and formal verification are increasingly interconnected:
- **Fuzzers Learning from Verification**:
  - Techniques like symbolic execution are improving fuzzing’s ability to explore state spaces systematically.
  - Developers can use tools like symbolic debuggers to identify uncovered branches and guide fuzzing efforts.
  
- **Verification Simplified for Developers**:
  - Tools like Kontrol integrate formal verification into developer workflows by reusing property tests written in Solidity.
  - Innovations in user experience, such as visual debuggers, are making verification accessible to non-experts.

---

### **4. Real-World Examples**
- **Ethereum Deposit Contract** (Formal Verification): Runtime Verification uncovered a critical bug in the Vyper compiler while verifying the Ethereum deposit contract. The bug could have led to stakers losing ETH. This issue was unlikely to be caught by fuzzers, as it involved malformed inputs.
- **Exotic Libraries in DeFi** (Fuzzing): Eki used differential fuzzing to compare outputs from a rarely used Solidity math library against a Python equivalent. They discovered rounding precision issues, highlighting fuzzing’s value in quick validation without deep audits.

---

### **5. Final Recommendations for Developers**
1. **Start Writing Tests**: Unit tests, integration tests, and property tests lay the foundation for both fuzzing and verification.
2. **Embrace Fuzzing**: Use fuzzing tools like Foundry or Wake to find edge cases early and often.
3. **Explore Verification**: If you’re new to formal methods, start with accessible tools like Kontrol or guided symbolic debuggers.
4. **Iterate and Collaborate**:
   - Seek input from auditors, developers, and the community to refine specifications.
   - Use mutation testing and visual tools to increase test suite coverage.

---

### **Conclusion**
Both fuzzing and formal verification are indispensable for securing smart contracts. While fuzzing provides quick wins and often catches bugs for arithmetic and integration testing, formal verification ensures correctness for critical properties. As tooling continues to evolve, the lines between these approaches are blurring, making it an exciting time for developers to explore both.

**Take Action**:
- **Try Kontrol**: Reuse your fuzzing tests for formal verification.
- **Test with Foundry or Wake**: Start fuzzing today to harden your contracts.
- **Experiment with Symbolic Debuggers**: Visualize state spaces and uncover edge cases.

**The Future of Security**: As one panelist put it, the rapid innovation in this space means what’s cutting-edge today could be commonplace tomorrow. Don't wait—start integrating these tools into your workflow!

<iframe width="560" height="315" src="https://www.youtube.com/embed/NCclZjMmkDs?si=fWswXb61SISkqgjA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>