# **The Anthropic Disclosures: Inside the CoBench v2 Leap, the Silent 133M-Message Biosecurity Leak, and the Rise of "Model 2"**

##

Silicon Valley has long debated when the capability curve of frontier artificial intelligence would collide head-on with the limits of automated safety. That collision is no longer theoretical. Anthropic’s newly released **August 2026 Risk Report** (covering the period up to July 15, 2026) has dropped a series of bombshell disclosures, revealing the existence of an unreleased, highly capable internal system codenamed **"Model 2"** and documenting a major, 11-month biosecurity safety filter bypass that went entirely undetected at scale. 

For tech insiders, the report is an unsettling look at how the complexity of automated safety infrastructure is beginning to fail under the weight of rapid capability scaling. From proprietary engineering benchmarks to silent database configuration bugs, here is the technical deep dive into what occurred behind closed doors at Anthropic.

---

### The Engine: CoBench v2 and the "Model 2" Capability Leap

At the heart of the technical disclosures is **Model 2**, an internal-only model that Anthropic uses for research, training-data generation, and agentic engineering. Rather than relying on public benchmarks that have largely saturated, Anthropic evaluated Model 2 on **CoBench v2**—a proprietary, highly demanding evaluation suite consisting of 449 real-world AI research and development tasks previously solved by Anthropic's own human engineering staff.

```
CoBench v2 Evaluation Scores (%)
===================================
Claude Mythos 5:     ███████████████████ 50.3%
Claude Mythos Preview:█████████████████████ 54.8%
Model 2 (Internal):  ████████████████████████ 62.8%
-----------------------------------
AGI Substitution Threshold: ████████████████████████████████ 85.0%
```

Model 2 achieved a score of **62.8%** on CoBench v2, representing a major leap over the public-facing flagship **Claude Mythos 5** (which scored **50.3%**) and the **Mythos Preview** (which scored **54.8%**). While Claude Fable 5 serves as the general public release (incorporating heavy-handed classifiers that fall back to older models when sensitive topics are queried), Mythos 5 remains restricted due to its advanced capability profile. 

The 62.8% score is technically significant because of how CoBench is designed: it filters out tasks that the Mythos Preview can already handle reliably, focusing entirely on advanced, multi-step engineering challenges. Anthropic estimates that a model scoring **85%** on CoBench would be capable of fully substituting for its human technical research staff—essentially reaching a threshold where the AI can autonomously design, write, test, and execute its own training loops to self-improve.

On Reddit’s r/singularity, the capability gap sparked immediate debate. One popular thread analyzed whether Model 2 is currently the most capable coding engine on Earth. AI researcher and writer **Zvi Mowshowitz**, writing on his Substack *Don't Worry About the Vase*, noted that while Model 2 is still below the 85% autonomous replication threshold, a 62.8% score on CoBench is "remarkably high," adding that it confirms Model 2 is "likely the world's best AI model" currently locked behind closed doors.

---

### The Post-Mortem: Dissecting the 11-Month Biosecurity Bypass

While Model 2 represents a major capability jump, the most alarming disclosure in the August 2026 report is a critical software engineering flaw that left Anthropic’s biosecurity filters entirely disabled for nearly a year.

From **May 2025 to April 2026**, Anthropic’s biological and chemical weapons blocking classifiers were bypassed for all traffic originating from third-party human-feedback collection platforms. This safety lapse affected approximately **133 million AI interactions** involving roughly **50,000 external contractors**.

#### The Software Engineering Flaw
The root cause was a silent database configuration error. Traffic from human-feedback platforms was incorrectly tagged with an **`internal-use-only` flag**. 

In Anthropic's automated safety architecture, this flag was designed to allow internal researchers to test models without triggering real-time safety blocks. However, when applied to contractor platforms, it triggered a catastrophic "double-whammy" bug:
1. **Classifier Bypass:** The real-time biological and chemical weapons blocking classifiers were deactivated, allowing raw, unfiltered prompts to reach the model.
2. **Logging Deactivation:** The flag suppressed the logging and flagging pipeline. Because the interactions were classified as "internal," the standard safety-telemetry systems did not write triggers to the audit databases, preventing the automated alerting infrastructure from flagging the bypass.

```
Contractor Traffic Flow (May 2025 - April 2026)
-----------------------------------------------
[Contractor Prompt] 
       │
       ▼
[Ingress Gateway] ──► Sets "internal-use-only" flag (Configuration Bug)
       │
       ▼
[Safety Pipeline] ──► Bypasses Biosecurity Classifiers (No Active Blocking)
       │
       ▼
[Claude Engine]
       │
       ▼
[Response Generated] ──► Suppresses Logging & Alerts (No Telemetry Captured)
```

For 11 months, this silent failure remained completely undetected. It was only during a routine infrastructure audit in April 2026 that engineers discovered the misapplied database tag. 

Anthropic immediately launched a retrospective triage, reconstructing the unlogged transcripts from raw transaction caches. Out of the 133 million exchanges, the company identified **1,197 transcripts** that were flagged as "high risk." Fortunately, a manual review by biosecurity experts concluded that the interactions did not provide a "meaningful uplift" to a biological-weapons threat actor, as most were associated with deliberate internal red-teaming or benign academic inquiries. 

Yet, the governance fallout has been severe. Anthropic raised its internal risk ratings for both "non-novel chemical/biological threats" and "misalignment in high-stakes settings" (Threat Model 2) from **"very low" to "low."**

Zvi Mowshowitz criticized the scale of the oversight:
> "And by 'some' we mean almost a year of roughly 50,000 people and 133 million exchanges. Again, it's not only the mistake, it's that these mistakes often stick around so long, and get applied at such scales."

---

### Project Glasswing: Gated Defense vs. Open Release

The biosecurity lapse highlights the vulnerability of automated safety infrastructure at a time when frontier models are demonstrating dangerous capabilities. This capability risk is precisely why Anthropic has restricted Claude Mythos 5. 

During internal testing, Anthropic discovered that Mythos-class models had reached a level of coding and reasoning where they could autonomously discover, write exploits for, and chain together unrelated software vulnerabilities—effectively executing zero-day attacks against major operating systems and browsers.

Rather than releasing Mythos 5 publicly, Anthropic launched **Project Glasswing** in April 2026. Glasswing is an invite-only defensive initiative that provides vetted critical infrastructure partners with controlled access to Mythos 5. The program, which started with 50 partners, expanded to over 150 organizations by mid-2026, including AWS, Google, NVIDIA, CrowdStrike, Cloud Software Group (Citrix/TIBCO), and cryptocurrency exchange Kraken (Payward). 

Participating organizations use the advanced model to scan their massive codebases for deep-seated security flaws. By leveraging an AI capable of "vulnerability chaining," defensive teams can patch complex zero-day vectors before attackers can exploit them. 

---

### The Silicon Valley Governance Debate

The disclosures have ignited a fierce debate on X.com and Reddit regarding the governance of internal-only model testing and the viability of Responsible Scaling Policies (RSPs). 

#### 1. The Pragmatic View: Classic Software Flaws
Meta's Chief AI Scientist, **Yann LeCun**, took to X.com to argue that the biosecurity bypass proves that the existential dread surrounding AI is misplaced, pointing instead to standard software engineering hygiene:
> "Once again, the 'catastrophic' threat is a configuration mistake. AI safety isn't about alignment math or existential doom; it's about database hygiene and standard software testing. We are treating database bugs as existential crises."

#### 2. The Existential Warning: Recursive R&D
Conversely, safety researchers and former AI lab members see the CoBench scores as an alarm bell. Former OpenAI researcher **Leopold Aschenbrenner** warned that the rapid rise in automated R&D capabilities brings us dangerously close to the point of no return:
> "We are only 22 percentage points away from full research staff substitution on CoBench v2. Once a model hits 85% and can run its own training loops, the capability explosion begins. If we cannot secure a simple configuration flag on contractor platforms, how do we expect to secure a recursively self-improving superintelligence?"

#### 3. The Open-Source Critique
Silicon Valley venture capitalists have also weighed in, arguing that gated programs like Project Glasswing are counterproductive. Prominent VCs, including **Marc Andreessen**, have argued that keeping the most capable defensive tools locked inside an elite corporate cartel makes the world less secure:
> "Restricting access to the most capable defensive tools under the guise of safety only serves to consolidate power. Open source and open deployment are the only ways to crowdsource cybersecurity. Keeping these models locked up in elite coalitions is security theater that leaves the rest of the web vulnerable."

#### 4. The Executive Defense
Anthropic CEO **Dario Amodei** defended the decision to hold back Model 2 and restrict Mythos 5 under the RSP framework:
> "We will not deploy frontier capabilities without complete, validated predeployment assessments. The CoBench scores and the biosecurity filter lapse validate that our capability increases are outstripping our assurance systems. We must scale security alongside compute."

The August 2026 Risk Report proves that the frontier of AI development is no longer just about training larger networks. As models like Model 2 approach human-level engineering proficiency, the real bottleneck is no longer compute—it is the engineering of the safety systems designed to contain them.

***

# Highlight

## 4.1 Key Questions
1. How does Anthropic's internal CoBench v2 benchmark redefine how we measure the progress toward autonomous AI research staff?
2. What are the software architecture flaws that allowed the `internal-use-only` flag to bypass biosecurity filters and logging for 11 months undetected?
3. How does keeping powerful models restricted under Project Glasswing impact the balance between defensive and offensive cybersecurity?

## 4.2 Highlight Text
Anthropic’s August 2026 Risk Report has dropped a bombshell: the existence of "Model 2," an unreleased coding engine scoring a massive 62.8% on the internal CoBench v2 benchmark (compared to Claude Mythos 5’s 50.3%). Despite this capability jump, Anthropic is pausing external release under its RSP. Crucially, the report reveals an 11-month biosecurity safety filter bypass affecting 133M contractor interactions due to a misapplied "internal-use" flag. As the industry debates this silent failure, the lines are drawn between classic software configuration errors and the existential risks of recursive R&D automation.

## 4.3 Hashtags
#AISafety #Anthropic #CoBenchv2 #Model2 #Cybersecurity #ProjectGlasswing
