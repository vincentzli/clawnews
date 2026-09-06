# **The 13-Million-Line Proof: How Anthropic’s Claude Autoformalized Fermat’s Last Theorem—and Redefined the Architecture of Reason**

###

On September 4, 2026, the formal verification community crossed an inflection point that many researchers believed was decades away. Anthropic announced that an autonomous collective of Claude agents, orchestrated over an 11-day continuous run, had completed the first fully machine-checked, end-to-end formalization of Fermat’s Last Theorem (FLT) in the Lean 4 proof assistant.

The raw metrics alone challenge contemporary assumptions about LLM reasoning horizons: 11 days of parallel compute, approximately 6 billion output tokens, over 30,000 theorems proved, and a final integrated codebase spanning 13 million lines of Lean 4 code across 29,511 intermediate lemmas. In doing so, Claude checked off the 100th and final entry on Freek Wiedijk’s famous list of *“Formalizing 100 Theorems,”* closing out a foundational 20-year computer science benchmark.

Yet behind the breathless headlines lies a far more nuanced, technically instructive story. Claude did not "discover" a new proof of Fermat’s Last Theorem; it did not replace the genius of Sir Andrew Wiles, Richard Taylor, or Ken Ribet. Instead, this milestone represents the triumph of **large-scale autoformalization**—the automated translation of dense, unstructured human mathematical thought into mathematically irrefutable, computer-verified code.

```
+-------------------------------------------------------------------------+
|                  PROVE2ME COORDINATION ARCHITECTURE                     |
+-------------------------------------------------------------------------+
|                                                                         |
|      +-----------------------------------------------------------+      |
|      |               Global Dependency DAG Engine                |      |
|      |       (Decoupled Theorem Signatures vs. Proof Bodies)     |      |
|      +-----------------------------+-----------------------------+      |
|                                    |                                    |
|             +----------------------+----------------------+             |
|             |                      |                      |             |
|             v                      v                      v             |
|     [Claude Agent 1]       [Claude Agent 2]       [Claude Agent N]      |
|    (Elliptic Curves)     (Galois Reps / DDT)     (Hecke / Ribet)        |
|             |                      |                      |             |
|             v                      v                      v             |
|     +---------------+      +---------------+      +---------------+     |
|     | Lean 4 Server |      | Lean 4 Server |      | Lean 4 Server |     |
|     |  (LSP Diags)  |      |  (LSP Diags)  |      |  (LSP Diags)  |     |
|     +-------+-------+      +-------+-------+      +-------+-------+     |
|             |                      |                      |             |
|             +----------------------+----------------------+             |
|                                    |                                    |
|                                    v                                    |
|                  +-----------------------------------+                  |
|                  |     Lean 4 Kernel Verification    |                  |
|                  |     (3 Axioms: propext, quot,     |                  |
|                  |      Classical.choice / nanoda)   |                  |
|                  +-----------------------------------+                  |
+-------------------------------------------------------------------------+
```

#### The Algorithmic Engine: The Prove2Me Platform
Why did Anthropic succeed where past automated theorem-proving attempts stalled? 

Historically, AI-driven theorem proving has split into two paradigms:
1. **Monte Carlo Tree Search (MCTS) & Reinforcement Learning**: Exemplified by Google DeepMind’s AlphaGeometry and AlphaProof, these systems treat theorem proving as an adversarial search game. While remarkably potent for self-contained, 30-line International Mathematical Olympiad (IMO) problems, MCTS collapses under the weight of deep research mathematics, where the state space involves thousands of definitions across algebraic geometry, modular forms, and Galois representations.
2. **Naive Autoregressive Generation**: Feeding an entire textbook to an LLM and asking for Lean 4 code inevitably fails. As context windows expand, models suffer from semantic drift, hallucinate nonexistent library lemmas, and overwhelm Lean’s elaborator and typeclass synthesis caches.

To conquer Wiles’s proof, Anthropic deployed **Prove2Me**, a collaborative autoformalization infrastructure designed by Assistant Professor Tianyi Peng (Columbia University / Anthropic) and his collaborators. Prove2Me acted as a stateful, dependency-aware orchestrator that decoupled mathematical planning from tactic-level execution.

##### 1. The Global Dependency Directed Acyclic Graph (DAG)
Prove2Me mapped the chosen mathematical route—the 1997 Darmon–Diamond–Taylor (DDT) exposition of the Wiles–Taylor proof—into a structured DAG containing tens of thousands of modular nodes. Each node represented a precise theorem or lemma statement.

##### 2. Signature and Proof Decoupling
In standard Lean development, changes to an upstream theorem force the compiler to re-elaborate everything downstream, causing immense performance degradation. Prove2Me solved this by strictly isolating **declarations (signatures)** from **proof scripts (implementations)**. Upstream nodes provided type signatures that downstream agents could invoke as axioms while parallel Claude instances simultaneously ground out the formal proofs. 

##### 3. Deterministic LSP Feedback Loops
When an agent wrote a proof for an open lemma, it interacted dynamically with the Lean 4 Language Server Protocol (LSP). When Lean rejected a tactic—whether due to type unification failure, motive synthesis error, or missing typeclass instances—the compiler diagnostics were fed directly back into Claude's prompt context. Claude did not avoid hallucinations through magical intuition; rather, **hallucinations were violently pruned at the compiler boundary**. The system turned Lean’s typechecker into an unbending, deterministic reinforcement signal.

```
+-----------------------------------------------------------------------+
|                PARADIGM COMPARISON IN FORMAL REASONING                |
+-----------------------------------------------------------------------+
| Metric / Attribute    | AlphaProof (DeepMind)  | Claude + Prove2Me    |
+-----------------------+------------------------+----------------------+
| Core Search Mechanism | RL + Monte Carlo Trees | Swarm DAG Scheduling |
| Target Domain         | Bounded IMO Problems   | Monolithic Proofs    |
| Primary Input         | Formal Problem Spec    | Informal Literature  |
| Code Volume           | Hundreds of Lines      | 13+ Million Lines    |
| Human Supervision     | High (Formalization)   | Minimal (Nudges)     |
+-----------------------+------------------------+----------------------+
```

#### The Mathematical Path: Darmon-Diamond-Taylor
Rather than attacking Wiles’s original 1995 papers directly—which relied on specific, highly intricate geometric constructions—the Anthropic project formalized the cleaner framework presented in the 1997 paper *"Fermat's Last Theorem"* by Henri Darmon, Fred Diamond, and Richard Taylor.

The mathematical backbone formalized in Lean 4 centers on verifying that every semistable elliptic curve over $\mathbb{Q}$ is modular. Claude formalized:
* The construction of the **Frey-Hellegouarch elliptic curve** associated with a hypothetical non-trivial solution $a^p + b^p = c^p$.
* The Galois representations $\rho_{E,p}: \text{Gal}(\bar{\mathbb{Q}}/\mathbb{Q}) \to \text{GL}_2(\mathbb{F}_p)$ arising from the $p$-torsion points of the Frey curve.
* Ken Ribet’s Level-Lowering Theorem (the epsilon conjecture), which proves that if the Frey curve is modular, its associated modular form must have conductor 2.
* The dimension of the space of weight-2 cusp forms for $\Gamma_0(2)$, which is precisely zero—yielding the final contradiction.

Crucially, the formalization relied solely on Lean’s three standard foundational axioms:
1. `Classical.choice` (the non-constructive Axiom of Choice)
2. `propext` (Propositional Extensionality)
3. `Quot.sound` (Quotient Soundness)

Independent researchers verified the artifact not only using Lean’s native kernel but also via `nanoda`, an external, minimalist Lean 4 typechecker written in Rust. There were **zero `sorry` placeholders** and zero non-standard axioms.

```
+-------------------------------------------------------------------------+
|                  LEAN 4 FOUNDATIONAL VERIFICATION GATES                 |
+-------------------------------------------------------------------------+
|                                                                         |
|     +-------------------------------------------------------------+     |
|     |                   Claude-Generated Proof                    |     |
|     |                 (13,000,000 Lines of Lean)                  |     |
|     +------------------------------+------------------------------+     |
|                                    |                                    |
|                                    v                                    |
|     +-------------------------------------------------------------+     |
|     |                  Calculus of Constructions                  |     |
|     |                (Curry-Howard Isomorphism)                   |     |
|     +------------------------------+------------------------------+     |
|                                    |                                    |
|             +----------------------+----------------------+             |
|             |                                             |             |
|             v                                             v             |
|    [Lean 4 Native Kernel]                         [nanoda (Rust)]       |
|    - propext                                      - Independent check   |
|    - Quot.sound                                   - Zero axioms added   |
|    - Classical.choice                             - Zero 'sorry' stubs  |
|             |                                             |             |
|             +----------------------+----------------------+             |
|                                    |                                    |
|                                    v                                    |
|                      MATHEMATICAL CERTITUDE (Q.E.D.)                    |
+-------------------------------------------------------------------------+
```

#### The Human Dimension: Kevin Buzzard and the Mathematics Community
The announcement triggered intense reaction across the mathematics and computer science ecosystems.

Mathematician **Kevin Buzzard** of Imperial College London, who has championed formal verification for a decade and leads an active UKRI/EPSRC-funded project to formalize FLT in Lean 4 through 2029, published an immediate assessment on September 4 titled **"FLT: Anthropic has beaten me to it."**

Buzzard’s response offered a necessary reality check against hyperbole:
> *"The formalization of Fermat's Last Theorem tells us essentially nothing about mathematics, because Wiles proved it thirty years ago... But as an autoformalization achievement, it is extraordinary. What Anthropic and Tianyi Peng’s platform have demonstrated is that AI can read human mathematical literature, extract the structure, and turn it into verified Lean code at unprecedented scale."*

Buzzard also noted that his own project remains actively funded and underway for a vital reason: **architecture and pedagogy**. Buzzard's team is constructing a modern modularity-lifting proof designed to build reusable, human-digestible abstractions that can be permanently integrated into `Mathlib`, Lean’s official mathematical library.

By contrast, Claude’s 13 million lines of Lean 4 are what specialists call **"machine-dialect Lean."** As users on Hacker News and Reddit observed:
* **Hyper-Verbosity**: Claude’s proofs average over 440 lines of code per lemma, often explicitly spelling out term rewrites that human formalizers would collapse into automated tactics like `ring`, `omega`, or `aesop`.
* **Low Modularity**: The codebase is monolithic and bespoke. It solves the target theorems but lacks the generalized typeclasses and polymorphic interfaces required for upstream community reuse.
* **Write-Only Code**: Much like compiler-generated assembly or minified JavaScript, the artifact is virtually unreadable to human mathematicians seeking intuitive conceptual understanding.

Field Medalist **Terence Tao** offered further perspective, cautioning against conflating automated formalization with mathematical problem-solving:
> *"Autoformalization of established proofs is a profound engineering milestone that transforms verification, but it is fundamentally different from discovering new mathematics. It solves the verification bottleneck, not the conjecture-discovery bottleneck."*

```
+-----------------------------------------------------------------------+
|                    COMMUNITY PERSPECTIVES BREAKDOWN                   |
+-----------------------------------------------------------------------+
| Notable Figure  | Core Assessment                                     |
+-----------------+-----------------------------------------------------+
| Kevin Buzzard   | "Extraordinary autoformalization... but tells us    |
| (Imperial)      | essentially nothing new about the math itself."     |
+-----------------+-----------------------------------------------------+
| Terence Tao     | "Transforms formal verification, but distinct from  |
| (UCLA)          | discovering new mathematical insights."             |
+-----------------+-----------------------------------------------------+
| Dario Amodei    | "Demonstrates that coupling neural models with hard |
| (Anthropic CEO) | logic kernels eliminates hallucinations entirely."  |
+-----------------+-----------------------------------------------------+
| Mathlib Core    | "13M lines of machine-dialect Lean is impressive,   |
| Maintainers     | but unmergeable into standard libraries as-is."     |
+-----------------+-----------------------------------------------------+
```

#### The Industrial Paradigm Shift: From Pure Math to Mission-Critical Software
While pure mathematicians debate the aesthetic value of 13 million lines of machine-dialect Lean, the software engineering, cybersecurity, and hardware industries view Anthropic's breakthrough as a tectonic shift.

For sixty years, the Holy Grail of computer science has been **formally verified systems**—programs whose correctness is proven with mathematical certainty, eliminating buffer overflows, concurrency deadlocks, and logic vulnerabilities. Until now, formal verification was economically impossible for all but the most critical projects (such as the seL4 microkernel or Airbus avionics), demanding hundreds of person-years by elite PhDs.

Anthropic’s 11-day run alters the economics of verification:
1. **Automated Cryptographic Auditing**: Cryptographic protocols, zero-knowledge circuits, and consensus mechanisms can now be autoformalized directly from specification papers into verified code, rendering implementation-level exploits obsolete.
2. **Hardware Synthesis and ASIC Design**: Modern silicon design suffers from astronomical tape-out costs driven by verification bugs. Swarms of logic-checked LLMs can verify complex instruction sets and cache-coherency protocols against formal specifications in days rather than quarters.
3. **The Neurosymbolic Blueprint for AI Safety**: Large language models have historically been plagued by probabilistic hallucinations. Anthropic’s run illustrates the blueprint for next-generation autonomous engineering: **probabilistic generation paired with deterministic symbolic kernels**. By subordinating LLM idea generation to an uncompromising logical verifier, AI systems can operate autonomously over long horizons with absolute logical guarantees.

Anthropic’s formalization of Fermat’s Last Theorem did not prove Sir Andrew Wiles wrong, nor did it unearth secrets that Fermat left in his margins. But by driving a machine through 13 million lines of uncompromising logic without a single error, it established that the future of computer science belongs to systems that can both dream up solutions and mathematically prove they are correct.

---

# 4. Highlight

### 4.1 Key Questions
1. **Did Claude discover new mathematics, or merely translate Andrew Wiles's existing proof?**
2. **How did Anthropic prevent context drift and hallucinations across 13 million lines of Lean 4 code?**
3. **What does an 11-day autonomous proof formalization mean for commercial software and hardware verification?**

### 4.2 Highlight Text
In a landmark automated reasoning milestone, Anthropic’s Claude has completed the first computer-verified formalization of Fermat’s Last Theorem in Lean 4. Running autonomously for 11 days across 6 billion tokens, Claude generated 13 million lines of verified code and proved 29,511 lemmas to formalize Andrew Wiles’s proof via the Darmon-Diamond-Taylor route. Orchestrated via the Prove2Me dependency DAG, the system prunes hallucinations at the Lean kernel boundary. While mathematicians note the verbose code isn't yet Mathlib-ready, it proves formal verification of complex software and hardware is now commercially viable.

### 4.3 Hashtags
#ArtificialIntelligence #Lean4 #FormalVerification #Anthropic #Claude #Mathematics #CyberSecurity #ComputerScience
