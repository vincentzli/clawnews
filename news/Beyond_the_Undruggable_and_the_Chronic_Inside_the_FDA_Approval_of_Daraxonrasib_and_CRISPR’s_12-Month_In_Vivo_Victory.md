# **Beyond the Undruggable and the Chronic: Inside the FDA Approval of Daraxonrasib and CRISPR’s 12-Month In Vivo Victory**

####

For forty years, molecular oncology hit a dead end known as the RAS superfamily. Accounting for roughly a quarter of all human malignancies—and over 90% of lethal pancreatic ductal adenocarcinomas (PDAC)—RAS proteins were labeled "undruggable." Their sub-nanomolar affinity for GTP, combined with a smooth, globular tertiary topology devoid of deep allosteric pockets, defeated traditional medicinal chemistry. Simultaneously, in genetic medicine, the holy grail of *in vivo* somatic gene editing remained bottlenecked by delivery kinetics, transient enzyme exposure, and long-term durability concerns.

That era ended this week across two historic clinical milestones: the FDA accelerated approval of daraxonrasib (brand name Rasonque, developed by Revolution Medicines) as the first true pan-RAS inhibitor, and the *New England Journal of Medicine* (NEJM) publication of 12-month Phase 1 durability data for CTX310 (CRISPR Therapeutics), an *in vivo* CRISPR-Cas9 lipid nanoparticle (LNP) therapy targeting *ANGPTL3*.

Together, these breakthroughs signal a fundamental architectural pivot in biotechnology: small molecules are becoming dynamic macromolecular glues capable of targeting multi-state protein complexes, while genetic medicine is graduating from *ex vivo* rare-disease cell therapies to one-and-done *in vivo* metabolic reprogramming for mass populations.

---

### Part I: Daraxonrasib and the Biophysical Conquest of Pan-RAS

The primary limitation of first-generation KRAS inhibitors (such as sotorasib and adagrasib) was their narrow allele specificity. They relied on covalent trapping of mutant cysteine residues in KRAS G12C, sequestering the protein solely in its inactive, GDP-bound (OFF) state. However, in pancreatic cancer, KRAS G12C accounts for less than 2% of cases. The overwhelming majority of PDAC tumors harbor G12D (~40%) or G12V (~30%) mutations, which lack a reactive cysteine thiol and remain persistently locked in the GTP-bound, active (ON) conformation.

Daraxonrasib (RMC-6236) circumvents this biophysical roadblock via a chaperone-mediated **tri-complex inhibitor** mechanism:

```
[ Daraxonrasib ] + [ Cyclophilin A (CypA) ]
                      │
                      ▼
       [ Binary Complex: Drug-CypA ]
                      │
                      ▼  (Engages active effector loop)
[ Tri-Complex: CypA · Daraxonrasib · RAS(ON/OFF) ]
                      │
                      ▼
  [ Steric Blockade of Downstream RAF / PI3K Signaling ]
```

Instead of seeking a non-existent deep cleft on naked RAS, daraxonrasib acts as a non-covalent molecular glue. It recruits the abundant endogenous chaperone protein Cyclophilin A (CypA / PPIA) with sub-nanomolar affinity. This binary drug–CypA complex generates a neo-surface that interfaces with the Switch-I and Switch-II loops of RAS. By creating massive steric hindrance, the complex prevents RAS from docking with its downstream effectors—namely RAF kinases in the MAPK pathway and PI3K in the AKT pathway. Crucially, because CypA recognizes conserved structural motifs across the active (GTP-bound) and inactive (GDP-bound) states, daraxonrasib inhibits mutant variants (G12D, G12V, G12R, G13X, Q61X) as well as wild-type KRAS, NRAS, and HRAS.

#### The Clinical Data: Phase 3 RASolute 302
In the pivotal Phase 3 RASolute 302 trial (NCT06625320) in patients with previously treated metastatic PDAC:
* **Overall Survival (OS):** Median OS reached **13.2 months** with daraxonrasib versus **6.7 months** on investigator’s choice chemotherapy (Hazard Ratio [HR] = 0.40; $p < 0.0001$).
* **Progression-Free Survival (PFS):** Median PFS was **7.2 months** vs. **3.6 months** (HR = 0.49; $p < 0.0001$).
* **Objective Response Rate (ORR):** 30% in the daraxonrasib arm versus 11% in the control arm.
* **Tolerability:** Treatment-related adverse event (TRAE) discontinuations were limited to **1.2%** for daraxonrasib compared to **11.2%** for cytotoxic chemotherapy. Common on-target toxicities (e.g., maculopapular rash, stomatitis, diarrhea) were predominantly Grade 1/2 and manageable via dose titration.

As veteran medicinal chemist and *In the Pipeline* author Derek Lowe noted regarding tri-complex pharmacology:
> *"Targeting the ON-state of RAS by borrowing an endogenous chaperone protein to sterically mask the effector binding site is one of the most intellectually elegant solutions to an 'impossible' target in modern drug discovery. It transforms the protein's flat surface into an asset rather than an insurmountable barrier."*

On biotech investor channels and X.com, discussions emphasized the commercial valuation of pan-RAS oncology. Alexis Borisy, veteran biotech founder and Chairman at Curie.Bio, remarked:
> *"The market spent twenty years convinced RAS was an unassailable fortress. First we breached G12C with covalent chemistry, but RMC-6236's approval in second-line pancreatic cancer proves that molecular glues can dismantle entire oncogenic hubs across broad patient populations."*

---

### Part II: CTX310 and In Vivo CRISPR-Cas9 Epigenetic/Genomic Rewriting

While daraxonrasib tackles the oncogenic core, the NEJM publication of CRISPR Therapeutics' Phase 1a/1b trial of **CTX310** establishes the clinical viability of *in vivo* gene disruption for chronic cardiometabolic diseases.

Targeting **ANGPTL3** (Angiopoietin-like protein 3)—a hepatocyte-secreted glycoprotein that inhibits lipoprotein lipase (LPL) and endothelial lipase (EL)—CTX310 aims to recreate the cardioprotective phenotype observed in individuals with natural loss-of-function mutations (familial hypobetalipoproteinemia), who display lifelong ultra-low levels of LDL-C and triglycerides without adverse hepatic or metabolic liabilities.

#### Mechanistic Delivery Architecture: Liver-Tropic LNPs
The delivery vehicle is an intravenously administered lipid nanoparticle engineered for hepatocyte tropism:
1. **Nanoparticle Composition:** Formulated with an ionizable amino-lipid (apparent $pK_a \approx 6.2 - 6.8$), helper phospholipid (DSPC), cholesterol, and a PEG-conjugated lipid.
2. **ApoE Opsonization & Endocytosis:** Upon systemic infusion, the neutral surface charge in physiological circulation recruits endogenous Apolipoprotein E (ApoE). This protein corona drives receptor-mediated endocytosis via the Low-Density Lipoprotein Receptor (LDLR) on hepatic parenchymal cells.
3. **Endosomal Escape & Translation:** Acidification inside the endosome protonates the ionizable lipid, inducing hexagonal phase transition and endosomal membrane disruption. The single-guide RNA (sgRNA) and codon-optimized *Streptococcus pyogenes* Cas9 (SpCas9) mRNA are released into the cytoplasm.
4. **Permanent Disruption:** SpCas9 is translated, binds the sgRNA, translocates into the nucleus, and induces a targeted double-strand break (DSB) within exon 1 of *ANGPTL3*. Error-prone non-homologous end joining (NHEJ) generates frameshift indels, permanently silencing the gene.

```
Intravenous LNP Infusion 
   ──► ApoE Corona Formation 
   ──► LDLR-Mediated Hepatocyte Uptake 
   ──► Endosomal Escape & Cas9 Translation 
   ──► Targeted DSB in ANGPTL3 Exon 1 
   ──► NHEJ Frameshift Knockout 
   ──► Permanent Clearance of Circulating ANGPTL3
```

#### 12-Month Durability Endpoints
The *NEJM* 1-year follow-up dataset demonstrated unprecedented single-dose durability:
* **Circulating ANGPTL3 Protein:** Mean reduction of **79.0%** (maximum 89.0%) from baseline at the optimal dose.
* **Low-Density Lipoprotein Cholesterol (LDL-C):** Durable reduction of **52.5%** (maximum 84.0%).
* **Serum Triglycerides (TG):** Sustained reduction of **47.8%** (maximum 78.0%).
* **Safety & Hepatotoxicity:** Transient, subclinical grade 1 transaminase elevations (ALT/AST) peaked at day 7 and normalized by day 28. No off-target indels were detected in high-depth circularized-sequencing assays, and zero treatment-related serious adverse events (SAEs) occurred.

Dr. Fyodor Urnov, Scientific Director at the Innovative Genomics Institute (IGI) at UC Berkeley, commented on X.com:
> *"The transition of CRISPR from ex vivo bone marrow transplant protocols to a routine 30-minute IV infusion that permanently rewrites a cardiovascular risk factor with 12-month flatline durability is the moment somatic gene editing moves from bespoke curative medicine to global preventive health."*

Similarly, Dr. Samarth Kulkarni, CEO of CRISPR Therapeutics, stated during the data presentation:
> *"A single intervention yielding more than 50% LDL-C reduction and nearly 50% triglyceride reduction sustained across an entire year fundamentally challenges the compliance-heavy, lifelong statin and antibody injection paradigm."*

---

### Part III: The FDA’s "Plausible-Mechanism" Regulatory Paradigm

The confluence of daraxonrasib’s approval and CTX310’s clinical maturation underscores a transformative shift in regulatory science. In February 2026, the FDA formalized its **Plausible-Mechanism Framework** alongside updated guidance on *Leveraging Prior Knowledge for Platform Technologies*.

Traditionally, changing a single nucleotide in a genetic therapy or switching an oncology molecule across related mutation sets required de novo preclinical and Phase 1 IND toxicity packages. Under the modular platform framework:
* **Component Decoupling:** Regulators now recognize the modularity of delivery systems (such as validated liver-tropic LNPs) and catalytic engines (Cas9 nuclease, cyclophilin-binding small molecule scaffolds).
* **Cross-Product Bridging:** When the safety and biodistribution profile of the platform backbone has been established, clinical trials can focus on guide-sequence specificity, target engagement confirmation, and disease-relevant biochemical markers rather than re-evaluating baseline delivery toxicology.
* **Master Protocols & Accelerated Pathways:** This framework paves the way for umbrella protocols where therapies targeting rare sub-mutations or combined metabolic pathways can obtain market clearance through biomarker-driven plausible mechanisms backed by external natural history controls.

As biopharma policy analyst Peter Kolchinsky, Managing Partner at RA Capital, summarized on Reddit’s r/biotech:
> *"The FDA is finally treating biotechnology like software engineering: once the runtime environment and delivery stack (the LNP or molecular glue backbone) are certified, swapping the payload logic shouldn't require rebuilding the compiler from scratch."*

```
Traditional Paradigm:
[ New Guide / Variant ] ──► [ Full Preclinical Tox ] ──► [ Phase 1 ] ──► [ Phase 2 ] ──► [ Phase 3 ]

Plausible-Mechanism Platform Paradigm:
[ Validated Delivery Backbone + Prior Platform Data ] + [ Target-Specific Payload ]
                               │
                               ▼
  [ Streamlined Mechanistic & Target Engagement Trial ] ──► [ Accelerated Market Access ]
```

---

### The Engineering Horizon

The simultaneous validation of pan-RAS inhibition and *in vivo* CRISPR disruption redefines the boundary conditions of translational medicine. 

In oncology, daraxonrasib dismantles the dogma that intracellular multi-protein interfaces cannot be blocked by small molecules without covalent handles. In genetic medicine, CTX310 proves that lipid nanoparticle delivery of RNA-guided nucleases can achieve sustained therapeutic knockdown in high-turnover tissue without genomic instability or chronic immune clearance.

For tech leaders, bio-engineers, and investors, the implications are unambiguous: the future of drug design belongs to multi-component molecular machines and modular genetic operating systems that convert chronic pathology into permanently corrected code.

---

### 4. Highlight

#### 4.1 Key Questions
1. How does daraxonrasib (Rasonque) drug the "undruggable" RAS superfamily across non-G12C variants like G12D and G12V?
2. What are the clinical endpoints and molecular delivery mechanics behind CTX310's 12-month *in vivo* CRISPR lipid reduction?
3. How does the FDA's new Plausible-Mechanism Framework transform modular gene editing and multi-target biotech platforms?

#### 4.2 Highlight Text
Biotech just crossed two historic milestones: the FDA approved **daraxonrasib (Rasonque)**—the first pan-RAS(ON/OFF) molecular glue doubling survival in metastatic pancreatic cancer (OS 13.2 vs 6.7 mos, HR 0.40)—while NEJM published 12-month Phase 1 data for **CTX310**, an *in vivo* CRISPR-Cas9 LNP therapy cutting LDL-C by 52.5% and triglycerides by 47.8% in a single infusion. Paired with the FDA’s new Plausible-Mechanism Framework, drug development is shifting from chronic disease maintenance to programmable, modular genomic cures.

#### 4.3 Hashtags
#Biotech #CRISPR #Oncology #GeneEditing #Pharma #PancreaticCancer #MolecularGlues
