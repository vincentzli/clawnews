# Beyond TOPO-1: How Novartis’s $1.5B Myricx Acquisition Re-Engineers the ADC Resistance Landscape

###

On July 6, 2026, Novartis shook the oncology landscape by announcing the acquisition of London-based Myricx Bio for up to $1.5 billion—comprising a massive $1.1 billion upfront cash payment and $400 million in development and commercial milestones. Historically, Novartis’s oncology crown jewel has been its pioneering work in **Radioligand Therapies (RLTs)**—spearheaded by the commercial blockbusters Pluvicto (177Lu-PSMA-617) for metastatic castration-resistant prostate cancer (mCRPC) and Lutathera (177Lu-DOTATATE) for neuroendocrine tumors. 

While RLTs represent a highly targeted, clinically validated modality, they are plagued by severe real-world operational bottlenecks. RLT supply chains are notoriously fragile, requiring just-in-time manufacturing due to the rapid radioactive decay of Lutetium-177 (half-life of ~6.7 days) and Actinium-225 (half-life of ~9.9 days). Furthermore, patients must be treated in specialized nuclear medicine facilities, limiting market penetration.

By contrast, **Antibody-Drug Conjugates (ADCs)** offer an "off-the-shelf" biological alternative. However, the first-generation ADC space has become fiercely crowded. Daiichi Sankyo and AstraZeneca dominate the topoisomerase-1 inhibitor (TOPO-1i) field with Enhertu (trastuzumab deruxtecan), while Pfizer (via its $43B Seagen acquisition) and AbbVie (via its $10.1B ImmunoGen acquisition) command the microtubule inhibitor (MMAE, DM4) domains. 

Rather than licensing or acquiring a late-stage, "me-too" TOPO-1i or tubulin-binding candidate, Novartis has chosen to leapfrog the competition. The Myricx acquisition is not just a commercial expansion; it is a profound pivot toward a proprietary, first-in-class payload chemistry platform: **N-myristoyltransferase inhibitors (NMTi)**. 

#### Molecular Mechanics: NMT Inhibition as a Cytotoxic Engine

To understand why Novartis is paying a premium for Myricx, one must look at the biochemistry of the payload. N-myristoyltransferase (NMT) is an essential eukaryotic monomeric enzyme (encoded by two genes in humans: *NMT1* and *NMT2*) that catalyzes the co-translational and post-translational attachment of myristate, a 14-carbon saturated fatty acid, to the N-terminal glycine residues of target proteins (N-myristoylation).

```
          Myristoyl-CoA + H2N-Gly-Protein
                        │
                        ▼  [N-myristoyltransferase (NMT1/2)]
          Myristoyl-NH-Gly-Protein + CoA-SH
```

Myristoylation acts as a hydrophobic anchor, enabling these proteins to translocate to lipid bilayers (plasma, nuclear, or organelle membranes) where they participate in signal transduction, membrane trafficking, and cellular survival. NMT has over 100 known substrates, including:

1. **Src-Family Kinases (SFKs):** Src, Yes, Fyn, Lyn, Lck, Hck, Fgr, and Blk. Myristoylation is required for their membrane localization. Without it, they cannot interact with receptor tyrosine kinases (e.g., EGFR, HER2) to propagate survival signals through the PI3K/Akt and MAPK pathways.
2. **ADP-ribosylation Factors (ARFs):** Critical regulators of vesicle budding, receptor internalization, and intracellular trafficking.
3. **G-Protein Alpha Subunits:** Modulating G-protein coupled receptor (GPCR) cascades.
4. **BID:** A pro-apoptotic Bcl-2 family member whose myristoylation regulates its translocation to the mitochondria to trigger cell death under stress.

When Myricx’s NMTi payload is internalized by the cancer cell, it binds selectively to the peptide-binding pocket of NMT, blocking substrate binding. This induces a multi-system cellular failure:

* **Signal Transduction Collapse:** SFKs are mislocalized to the cytosol, halting growth factor signaling.
* **Vesicular Traffic Freeze:** Receptors cannot recycle, and membrane integrity decays.
* **Apoptosis Induction:** The cells undergo mitotic arrest and trigger mitochondrial outer membrane permeabilization (MOMP), inducing rapid, clean cell death.

#### Orthogonality: Smashing the Barriers of TOPO-1 and Tubulin Resistance

In clinical oncology, the primary limitation of modern ADCs is acquired resistance. Patients treated with Enhertu or Trodelvy (sacituzumab govitecan) inevitably relapse. The molecular pathways of this resistance are well-documented:

* **MDR1/ABCB1 Efflux Pumps:** Cancer cells upregulate P-glycoprotein (MDR1) and Breast Cancer Resistance Protein (BCRP), which actively pump chemotherapy-based payloads (such as DXd or SN-38) out of the cytoplasm.
* **Target Downregulation/Mutation:** Downregulation of Topoisomerase 1 or mutations in the *TOP1* gene (e.g., E418G) render TOPO-1i payloads useless. Similarly, tubulin mutations render microtubule inhibitors ineffective.
* **DNA Damage Repair (DDR) Adaptation:** Tumors upregulate homologous recombination (HR) or non-homologous end joining (NHEJ) pathways, neutralizing DNA double-strand breaks.

Herein lies the power of Myricx’s platform. NMT inhibition is an **orthogonal mechanism of action (MoA)**. It does not target DNA replication or spindle dynamics; it targets lipid-modification machinery.

Furthermore, Myricx has chemically optimized its NMTi payloads to evade the MDR1 efflux pump. In preclinical assays, cell lines that had acquired a 100-fold resistance to TOPO-1i ADCs (through ABCB1 upregulation or TOP1 mutation) remained fully sensitive to Myricx’s NMTi-ADCs. By delivering an orthogonal payload that is insensitive to efflux, Novartis can position these candidates as the ultimate "resistance-breaking" therapies for patients who have failed prior ADC lines.

#### Pipeline Deep Dive: MYX-2470 (B7-H3) and MYX-2449 (HER2)

Novartis gains control of two highly promising, preclinical-stage candidate programs:

* **MYX-2470 (B7-H3 NMTi-ADC):** B7-H3 (CD276) is an immune checkpoint molecule overexpressed in a wide range of aggressive solid tumors (prostate, pancreatic, ovarian, and small cell lung cancer) while showing highly restricted expression in normal healthy tissues. In patient-derived xenograft (PDX) models of advanced, metastatic castration-resistant prostate cancer (mCRPC) and small cell lung cancer (SCLC)—both settings notorious for poor response to immunotherapies—MYX-2470 demonstrated **complete and durable tumor regressions** at low microgram-per-kilogram doses.
* **MYX-2449 (HER2 NMTi-ADC):** Targeting HER2 is a crowded space, but MYX-2449 differentiates itself through two key properties: it shows robust activity in both HER2-high (IHC 3+) and HER2-low (IHC 1+/2+, ISH-) breast and gastric PDX models, and it features optimized membrane permeability for potent bystander activity. Crucially, MYX-2449 demonstrated an encouraging safety profile in non-human primates (cynomolgus monkeys), showing no signs of interstitial lung disease (ILD)—a notorious dose-limiting toxicity of Enhertu.

#### The r/biotech Debate: Host-Enzyme Inhibition vs. Systemic Toxicity Risks

While the biology is elegant, the biotechnology community on Reddit's r/biotech has voiced significant skepticism regarding the systemic safety profile of NMT inhibitors. N-myristoylation is a crucial housekeeping pathway. Because NMT1 and NMT2 are ubiquitously expressed in healthy human organs, the therapeutic index of an NMTi-ADC is under intense scrutiny.

As one senior scientist commented on r/biotech:
> *"Myristoylation is involved in everything from cell-cell adhesion to mitochondrial homeostasis. If you have an ADC with a cleavable linker, and it leaks in the plasma, you aren't just looking at standard myelosuppression. You could be looking at systemic failure of the endothelial lining, cardiomyopathy, or severe peripheral neuropathies."*

Biotech researchers point to the clinical data of Pacylex Pharmaceuticals’ oral NMT inhibitor, **zelenirstat**, to address this concern. Zelenirstat, a small-molecule systemic NMTi, is currently in Phase 1 trials for hematologic malignancies. The preliminary clinical data showed that zelenirstat was well-tolerated with no dose-limiting toxicities at the recommended Phase 2 dose. This suggests that cancer cells, due to their hyper-proliferative state and reliance on myristoylated signaling proteins (like Src), are far more sensitive to NMT inhibition than quiescent, healthy cells.

When delivered via an ADC, the therapeutic window is theoretically widened even further. The antibody acts as a homing missile, concentrating the NMTi payload within the lysosome of the tumor cell. 

However, as another user highlighted:
> *"The therapeutic window will live or die by the linker chemistry. If Novartis uses a standard cleavable peptide linker that undergoes carboxylesterase-mediated cleavage in the circulation, the systemic release of a highly potent NMTi could be disastrous. Novartis will need to demonstrate that their linkers are ultra-stable in human plasma, far exceeding the stability profiles of standard valine-citrulline or GGFG linkers."*

#### Financial Structuring and the 2026 M&A Landscape

The financial terms of the deal—**$1.1 billion upfront in cash and $400 million in milestones**—reveal a highly aggressive and upfront-weighted structure. In early-stage biotech M&As, it is common to see heavily back-weighted deals (e.g., $100 million upfront and $1.4 billion in milestones) to mitigate the massive risk of preclinical assets failing in Phase 1. 

By paying **73.3% of the total deal value upfront in cash**, Novartis is signaling intense bidding pressure in the 2026 ADC market, where Big Pharma is desperate to secure "resistance-breaking" payloads. Novartis likely had to outbid several oncology-focused rivals (such as Merck, AbbVie, or J&J) who are desperate to secure these assets.

This transaction caps off a multi-year M&A surge in the ADC sector:

| Acquirer | Target | Deal Value | Lead Asset Phase / Target | Payload Class | Year |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Pfizer** | Seagen | $43 Billion | Approved (PADCEV, Adcetris) | Tubulin Inhibitor (MMAE) | 2023 |
| **AbbVie** | ImmunoGen | $10.1 Billion | Approved (ELAHERE) | Tubulin Inhibitor (DM4) | 2023 |
| **J&J** | Ambrx | $2 Billion | Phase 1/2 (ARX517 / PSMA) | Tubulin Inhibitor (MMAF) | 2024 |
| **Novartis** | Myricx Bio | **$1.5 Billion** | Preclinical (MYX-2470 / MYX-2449) | **NMT Inhibitor (NMTi)** | **2026** |

Novartis’s $1.5 billion acquisition of a preclinical platform is exceptionally premium compared to J&J’s $2 billion acquisition of Ambrx (which had clinical-stage assets). As Michael Bauer, Partner at Novo Holdings (which co-led Myricx’s £90M Series A in 2024 alongside Abingworth), previously noted: *"The scientific rationale behind Myricx's novel payload chemistry gives us confidence that NMTi ADCs have the potential to greatly expand the current repertoire of ADC applications beyond the current standard-of-care payload classes."*

#### Competitive Landscape & Market Positioning

Novartis plans to position Myricx’s candidates strategically against a formidable array of clinical-stage and approved rivals:

* **The B7-H3 Battlefield:** Daiichi Sankyo and Merck’s **ifinatamab deruxtecan (I-DXd / DS-7300)** is the front-runner, currently in Phase 3 trials (*IDeate-Lung02*) for small cell lung cancer (SCLC) and holding FDA Breakthrough Therapy Designation. BioNTech and DualityBio’s **BNT324/DB-1311** is advancing rapidly in metastatic castration-resistant prostate cancer (mCRPC). Both utilize Topoisomerase 1 inhibitor payloads. Novartis plans to position **MYX-2470** as the primary second-line treatment, using its NMTi payload to bypass these DNA-centric resistance mechanisms.
* **The HER2 Battlefield:** **Enhertu** (trastuzumab deruxtecan) is the gold standard for HER2-positive and HER2-low breast and gastric cancers. Novartis is positioning **MYX-2449** for the post-Enhertu setting. By exploiting the orthogonal NMTi MoA, MYX-2449 can eradicate tumor clones that have escaped Enhertu treatment due to loss of TOPO-1 sensitivity or upregulation of multidrug resistance proteins.

#### Conclusion: A High-Stakes Bet on Biological Orthogonality

Novartis’s acquisition of Myricx Bio is one of the most scientifically interesting deals of 2026. It represents a bold shift away from the logistical headaches of radioligands and into the cutting edge of next-generation ADC payload chemistry. By targeting N-myristoyltransferase, Novartis is betting that biological orthogonality can break the back of tumor resistance to topoisomerase and tubulin inhibitors. 

The clinical translation of MYX-2470 and MYX-2449, expected to commence by the end of 2026, will be the ultimate test of this hypothesis. If Novartis can successfully navigate the systemic safety concerns and prove that their linkers can safely deliver an NMT inhibitor to the tumor lysosome, they will have secured a multi-billion-dollar therapeutic franchise that redefines the treatment paradigm for resistant solid tumors.

---

## 4. Highlight

### 4.1 Key Questions
1. **Can NMTi payloads maintain systemic safety?** While Pacylex's zelenirstat provides clinical proof-of-concept for systemic NMT inhibition, delivering NMT inhibitors via ADCs raises critical questions about linker stability and off-target toxicities in tissues expressing low levels of B7-H3 or HER2.
2. **Will NMTi successfully bypass clinical TOPO-1 resistance?** Although preclinical data shows MYX-2449 and MYX-2470 completely bypass topoisomerase-1 resistance and MDR1-mediated efflux, clinical validation in post-Enhertu patients remains the ultimate commercial hurdle.
3. **Is Novartis's pivot away from RLTs commercially justified?** Novartis is betting that the logistics and administration convenience of off-the-shelf ADCs outweigh the proven blockbusters of RLTs like Pluvicto.

### 4.2 Highlight Text
Novartis’s $1.5 billion acquisition of Myricx Bio marks a major strategic pivot toward next-generation Antibody-Drug Conjugates (ADCs) and away from the supply-chain bottlenecks of radioligand therapies. By acquiring Myricx’s first-in-class N-myristoyltransferase inhibitor (NMTi) payload platform, Novartis is bypassing the crowded topoisomerase-1 and tubulin-binding fields. Preclinical candidates MYX-2449 (HER2) and MYX-2470 (B7-H3) demonstrate complete regressions in models resistant to standard therapies. If Novartis's linkers can prevent systemic leakage of this ubiquitous enzyme inhibitor, NMTis could become the premier resistance-breaking oncology franchise of the decade.

### 4.3 Hashtags
#Biotech #Novartis #ADCs #CancerResearch #Oncology #PharmaMA
