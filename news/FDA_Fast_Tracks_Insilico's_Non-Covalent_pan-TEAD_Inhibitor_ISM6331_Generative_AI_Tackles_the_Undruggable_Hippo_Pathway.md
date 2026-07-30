# **FDA Fast Tracks Insilico's Non-Covalent pan-TEAD Inhibitor ISM6331: Generative AI Tackles the "Undruggable" Hippo Pathway**

####

The FDA’s decision to grant Fast Track Designation to Insilico Medicine’s ISM6331 is a landmark milestone for the generative AI drug discovery industry. Developed using Insilico's proprietary generative chemistry platform, Chemistry42, ISM6331 is a potential best-in-class, non-covalent pan-TEAD inhibitor. The Fast Track status covers the treatment of adult patients with advanced, unresectable malignant pleural mesothelioma (MPM) that has progressed after anti-PD-1 immunotherapy and platinum-based chemotherapy. 

This regulatory milestone is a key test case for the industry: Can generative AI design a molecule that successfully targets the Hippo pathway—a notoriously challenging oncology target—while avoiding the safety and resistance issues of traditional drug discovery methods?

##### The Biology: Hippo Signaling and the TEAD-YAP/TAZ Axis
The Hippo signaling pathway is a key regulator of organ size, tissue regeneration, and cellular homeostasis. Under physiological conditions, the pathway is active, initiating a kinase cascade (involving MST1/2 and LATS1/2) that phosphorylates and inactivates the transcriptional co-activators YAP (Yes-associated protein) and TAZ. In many aggressive solid tumors, particularly malignant pleural mesothelioma, this pathway is dysregulated. This dysregulation is frequently driven by loss-of-function mutations in the *NF2* gene (which encodes the tumor suppressor Merlin), occurring in approximately 40% of mesothelioma patients.

When the Hippo pathway is inactivated, unphosphorylated YAP and TAZ accumulate in the nucleus. Because YAP and TAZ lack DNA-binding domains, they must bind to TEAD (TEA Domain) transcription factors (TEAD1–4) to drive the transcription of genes promoting cell survival, metastasis, and resistance to therapy. 

Traditionally, transcription factors have been labeled "undruggable" due to their lack of well-defined active sites. However, TEAD transcription factors contain a highly conserved, deep hydrophobic pocket that binds a palmitic acid lipid—a post-translational modification known as palmitoylation. This palmitoylation is essential for TEAD structure and its interaction with YAP/TAZ. Blocking this pocket prevents the assembly of the oncogenic YAP/TAZ-TEAD complex, effectively silencing Hippo pathway output.

##### The Chemistry: Non-Covalent vs. Covalent Inhibition
Most TEAD inhibitors currently in clinical development, such as Vivace Therapeutics’ VT3989 and Ikena Oncology’s IK-930, rely on covalent inhibition. They form a covalent bond with a conserved cysteine residue (e.g., Cys367 on TEAD1) inside the palmitoylation pocket. While covalent binding yields strong target engagement, it presents several drawbacks:
*   **Off-target reactivity:** Covalent warheads (often acrylamides) can bind non-specifically to other cysteine residues in the proteome, causing off-target toxicities.
*   **Acquired resistance:** A single point mutation in the targeted cysteine (e.g., Cys367Tyr) can render a covalent inhibitor ineffective.
*   **Irreversible binding dynamics:** Continuous target inactivation can exacerbate systemic toxicities.

ISM6331 is a **non-covalent** pan-TEAD inhibitor. By binding reversibly to the palmitoylation pocket with high affinity, ISM6331 avoids the reactive warheads of covalent agents. The challenge, however, is achieving sufficient binding affinity and pocket occupancy across all four TEAD isoforms (pan-TEAD inhibition) without the thermodynamic boost of a covalent bond.

##### How Chemistry42 Generated ISM6331
Insilico utilized Chemistry42, its generative chemistry platform, to design ISM6331. Chemistry42 integrates over 40 generative models—including Generative Adversarial Networks (GANs), Variational Autoencoders (VAEs), and reinforcement learning—with physical chemistry descriptors and molecular docking engines. 

The AI was tasked with designing a molecule that met several constraints:
1.  High-affinity, non-covalent binding to the palmitoylation pocket of TEAD1–4.
2.  High selectivity against other palmitoylated proteins.
3.  Favorable ADME (Absorption, Distribution, Metabolism, and Excretion) properties, specifically oral bioavailability.
4.  Avoiding common reactive functional groups to minimize metabolic toxicity.

Chemistry42 generated novel molecular scaffolds that fit the hydrophobic palmitoylation pocket, optimizing hydrogen bonding networks and van der Waals interactions to achieve low nanomolar potency against TEAD1–4 without a covalent link. This design process significantly shortened the target-to-candidate timeline compared to traditional high-throughput screening (HTS) methods.

##### The Clinical Gauntlet and the Renal Question
ISM6331 is currently being evaluated in a global Phase I clinical trial (NCT06566079), which commenced in January 2025. The study is evaluating the safety, tolerability, pharmacokinetics, and preliminary efficacy of orally administered ISM6331 in patients with advanced solid tumors, focusing on mesothelioma. 

The primary technical hurdle for any TEAD inhibitor is **renal toxicity**. TEAD is highly expressed in the kidney, where the Hippo pathway regulates water homeostasis and renal tubule development. Covalent TEAD inhibitors have historically shown dose-limiting renal toxicities, such as proteinuria, hematuria, and tubular necrosis, in preclinical and early clinical studies. This has forced clinical protocols to adopt intermittent dosing schedules to allow renal tissue to recover.

Whether ISM6331's non-covalent binding profile and PK properties can decouple anti-tumor efficacy from renal toxicity remains the key question. The industry will get its first glimpse of the answer at the **ESMO 2026 Congress** in Madrid, where first-in-human data is scheduled for a Rapid Oral presentation on October 25, 2026.

##### Silicon Valley Debates: Tech CEOs, VCs, and Chemists
The progress of ISM6331 has sparked intense debate in the biotech and tech investment communities.

Alex Zhavoronkov, Founder and CEO of Insilico Medicine, has been vocal about the speed and efficiency of generative AI:
> "With Chemistry42, we didn't just search a library; we designed a molecule from scratch specifically tailored to block the TEAD palmitoylation pocket without requiring a covalent warhead. ISM6331 represents the first program in our AI-designed pipeline to achieve Fast Track Designation, validating our generative pipeline's capacity to deliver clinical-stage assets for notoriously difficult oncology targets."

Vijay Pande, General Partner at a16z Bio + Health, views this as a shift toward predictive bio-engineering:
> "The transition of biology from an empirical, discovery-based science to an engineering-based predictive discipline is happening right now. Generative AI allows us to move from brute-force screening to rational molecular compiler loops. Insilico's regulatory progress is an early indicator of this paradigm shift."

However, industry veterans remain cautious. Derek Lowe, a veteran medicinal chemist and author of *In the Pipeline*, highlights the translation gap:
> "TEAD is a classic example of a target that is structural rather than enzymatic. The industry has leaned heavily on covalent inhibitors targeting the conserved cysteine in the palmitoylation pocket. While covalent bonds give you strong binding, they also bring worries of off-target reactivity and resistance. Insilico's non-covalent approach is an interesting structural play, but the real test is in the kidneys. TEAD is heavily expressed in renal tissue, and dose-limiting renal toxicity has been the shadow hanging over this entire class. Can a generative-AI designed molecule escape this biological tax? We will see."

On Reddit's r/biotech, discussions focus on the clinical validation of AI:
> "We've seen dozens of AI-designed molecules enter Phase 1, but we're still waiting for the first major Phase 2 efficacy readout to prove that AI-designed drugs have a higher probability of clinical success. Chemistry42 is great at finding leads fast, but human clinical translation is the ultimate gatekeeper."

##### Investigative Outlook
The Fast Track Designation grants Insilico frequent FDA engagement, rolling reviews, and eligibility for accelerated approval pathways. This will accelerate development, but the clinical data remains the decider. If the upcoming presentation at the ESMO 2026 Congress demonstrates safety (especially the absence of severe renal toxicity) and preliminary efficacy in *NF2*-deficient patients, it will validate Insilico's non-covalent design strategy and support the broader generative AI drug discovery space.

---

### 4. Highlight

#### 4.1 Key Questions
1. How does a non-covalent binding mechanism compare to covalent inhibitors in terms of off-target toxicity and acquired drug resistance when targeting TEAD?
2. Can generative AI systems like Chemistry42 successfully predict and design around class-wide clinical liabilities like TEAD-related renal toxicity?
3. Will positive Phase I data from the upcoming ESMO 2026 presentation shift investor sentiment from skepticism to validation regarding generative AI pipelines?

#### 4.2 Highlight Text
The FDA has granted Fast Track Designation to Insilico Medicine's ISM6331, a non-covalent pan-TEAD inhibitor designed by Chemistry42 for malignant pleural mesothelioma. Unlike its covalent competitors, ISM6331 targets the TEAD palmitoylation pocket reversibly, aiming to avoid off-target toxicity and resistance mutations. However, the molecule must still navigate class-wide risks of renal toxicity. With Phase I clinical trials underway, the industry is looking toward the ESMO 2026 Congress this October for the first human data, which will serve as a key test for generative AI's clinical viability.

#### 4.3 Hashtags
#AIDrugDiscovery #Biotech #Oncology #GenerativeAI #Pharma Tech #Mesothelioma #FDA
