# Algorithms vs. the Blood-Brain Barrier: Inside Insilico’s $2.5 Billion Generative Biology Deal with SK Biopharm

####

At the BIO 2026 International Convention in San Diego on June 22, 2026, Insilico Medicine and SK Biopharmaceuticals announced a massive research and development collaboration valued at up to $2.5 billion. The partnership represents the largest APAC-focused AI drug discovery deal to date, aiming to tackle one of the most notoriously difficult frontiers in medicine: neuroimmune and central nervous system (CNS) disorders. Under the agreement, Insilico receives up to $18 million in upfront and near-term milestone payments, with the remaining deal value structured as development, regulatory, and commercial milestones, plus single-digit royalties on net sales.

The partnership relies on Insilico’s proprietary Pharma.AI generative biology and chemistry suite to discover novel therapeutic candidates, which SK Biopharmaceuticals will then license for late-stage clinical trials and global commercialization. The central mission? Overcoming the "CNS Chasm"—the historically high 99% attrition rate of central nervous system drug candidates due to the blood-brain barrier (BBB) and the complex biology of neuroinflammation.

##### The Tech Stack: PandaOmics, Chemistry42, and inClinico
Insilico’s end-to-end platform is split into three main programmatic modules:

1. **PandaOmics (Target Discovery)**: The platform identifies novel disease-associated targets by ingestion of multimodal omics data and millions of biomedical patents/publications. Its mathematical core is the **iPANDA** (Pathway Activation Network Decomposition Analysis) algorithm. iPANDA performs topological analysis on transcriptomic and proteomic datasets, decomposing network-level perturbations to identify which biological pathways are dysregulated in disease states. This is augmented by network diffusion models like **HeroWalk**, which map out how cellular signals propagate through protein-protein interaction networks to discover target candidates.

2. **Chemistry42 (Generative Chemistry)**: Once a target is selected, Chemistry42 utilizes an ensemble of over 42 generative algorithms—ranging from Generative Adversarial Networks (GANs) and Variational Autoencoders (VAEs) to evolutionary algorithms and reinforcement learning—to design *de novo* small molecules. For CNS targets, the generative reward functions are heavily weighted toward physical-chemical properties that dictate blood-brain barrier (BBB) penetration, such as polar surface area, molecular weight, charge, and logBB (the blood-brain partition coefficient). Physics-based simulation modules, including Free Energy Perturbation (FEP), predict binding affinity and ADMET (Absorption, Distribution, Metabolism, Excretion, and Toxicity) profiles.

3. **inClinico (Clinical Prediction)**: A transformer-based clinical trial simulation engine that leverages multimodal datasets—trial protocol structure, target biology, molecular attributes, and clinical history—to predict the Probability of Success (PoS) of Phase II to Phase III trials, helping to optimize protocol designs.

##### Preclinical and Clinical Efficacy Benchmarks
Insilico claims a 100% success rate in advancing nominated developmental candidates (DCs) to the IND-enabling stage (excluding strategic pipeline reprioritizations). By leveraging Pharma.AI, the company has slashed the timeline from target identification to preclinical candidate nomination from the traditional 4-6 years down to an average of 18 months. 

Its pipeline currently features 22 developmental candidates, with 10 clinical-stage assets. The flagship molecule, Rentosertib (ISM001-055), is a first-in-class small-molecule inhibitor of TNIK designed for Idiopathic Pulmonary Fibrosis (IPF). Rentosertib recently completed Phase IIa trials, showing positive safety signals and dose-dependent improvements in forced vital capacity (FVC). Additionally, their CNS-focused program, ISM8969, which is an orally available, brain-penetrant NLRP3 inflammasome inhibitor, has entered Phase I trials to study brain penetration in neurodegenerative models.

##### The Great Debate: Bits vs. Atoms and Clinical Translation
While the speed of preclinical generation is undisputed, the major industry debate centers on whether AI-designed molecules will actually translate to clinical success. 

"Short-term pessimist, long-term optimist," says Derek Lowe, a veteran medicinal chemist and writer of the influential blog *In the Pipeline*. Lowe has frequently argued that the primary bottlenecks in drug discovery are biological, not chemical. "The drug industry is messy and heartbreaking. AI can design a molecule that fits a pocket perfectly, but if the underlying biological hypothesis is wrong, the clinical trial will fail in Phase II or III. Computers cannot easily predict clinical surprises because biology is still a black box."

Daphne Koller, CEO of insitro, echoes these concerns, highlighting that many clinical failures occur because companies chase the wrong targets based on flawed biological hypotheses. Koller argues that the solution requires "fit-for-purpose" datasets rather than reliance on messy public databases.

Vijay Pande, General Partner at Andreessen Horowitz (a16z), sees the transition from "bits to atoms" as the ultimate test of the sector. Pande believes that using AI tools like inClinico to predict trial outcomes and optimize clinical protocols represents the "big win" for AI, where even a marginal bump in Phase II success rates could save billions of dollars.

For Insilico’s CEO, Alex Zhavoronkov, the math is simple: by slashing preclinical R&D times and costs, AI allows for more "shots on goal." Even if clinical trials remain a bottleneck, entering the clinic with more optimized molecules designed for target specificity and safety shifts the overall probability distribution in favor of success.

##### Restructuring R&D Budgets
Partnerships like this $2.5 billion collaboration are fundamentally restructuring R&D budgets across the biopharma sector. Traditionally, pharma companies spent massive capital maintaining in-house wet labs and high-throughput screening infrastructure. Today, we are seeing a shift toward an asset-light R&D model. Big Pharma is outsourcing early-stage discovery to AI platforms, shifting budgets from fixed preclinical overhead to clinical execution. In this model, upfront commitments are kept low ($18M in this deal) while "bio-bucks" (milestones) shift the financial weight onto late-stage clinical development and commercialization, where traditional players excel.

---

### 4. Highlight
#### 4.1 Key Questions
1. How do generative algorithms like Chemistry42 bypass the blood-brain barrier (BBB) by design?
2. Can predictive platforms like inClinico solve the Phase II/III clinical trial failure rate?
3. How is the shift to asset-light, AI-driven preclinical discovery restructuring Big Pharma's R&D capital allocation?

#### 4.2 Highlight Text
The $2.5 billion Insilico Medicine and SK Biopharmaceuticals partnership at BIO 2026 is a massive bet on generative biology solving the "CNS Chasm." By combining target discovery (PandaOmics' iPANDA algorithm) and generative chemistry (Chemistry42's GANs/RL) to optimize blood-brain barrier penetration, the duo aims to bypass traditional R&D attrition. While skeptics like Derek Lowe highlight that biological hypotheses remain a clinical bottleneck, the shifting economics of biopharma R&D are clear: upfront costs are shrinking, and R&D budgets are moving from fixed preclinical overhead to targeted clinical execution.

#### 4.3 Hashtags
#AIDrugDiscovery #GenerativeBiology #CNSTherapeutics #BiotechR&D #BIO2026 #MedTech
