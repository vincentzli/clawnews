# Mass Spec vs. Alzheimer’s: Inside the FDA’s Clearance of C2N's PrecivityAD2 and the Battle to Unclog the Neurological Pipeline

####

On August 20, 2026, the U.S. Food and Drug Administration (FDA) granted clearance to C2N Diagnostics’ PrecivityAD2® blood test. To the casual observer, it was just another diagnostic approval. But to those watching the intersection of biotech, clinical operations, and health economics, this was a watershed moment. PrecivityAD2 is the first FDA-cleared Alzheimer's blood test powered by high-resolution mass spectrometry (HRMS). It marks the transition of Alzheimer’s diagnostics from an expensive, invasive, and severely bottle-necked specialist pathway into a scalable, high-throughput molecular screening model.

With the recent approvals of disease-modifying monoclonal antibody (mAb) therapies like Eisai/Biogen’s Leqembi (lecanemab) and Eli Lilly’s Kisunla (donanemab), confirming brain amyloid pathology has become a multi-billion-dollar gatekeeping challenge. PrecivityAD2, utilizing an advanced statistical model called the Amyloid Probability Score 2 (APS2), delivers diagnostic accuracy that matches expensive PET scans and invasive lumbar punctures. But as healthcare networks rush to integrate these tests into electronic health records (EHR) via automated triage systems, a fierce debate is brewing over clinical access, reimbursement economics, and the limits of analytical platforms.

##### The Diagnostic Chokepoint: Why We Need a Blood Test
The clinical label for newly approved anti-amyloid mAbs is clear: patients must have documented evidence of brain amyloid plaques before treatment can begin. Historically, this meant undergoing either an amyloid PET scan or a cerebrospinal fluid (CSF) assay via lumbar puncture. 

In practice, this requirement has created an operational catastrophe. There are only about 2,000 active cognitive neurologists in the United States, tasked with managing a population of over 6.7 million Americans living with Alzheimer's. Waiting lists to see a specialist or secure a PET scan slot range from six to twelve months. Because these therapies are only indicated for patients in the mild cognitive impairment (MCI) or mild dementia stages, many patients progress past the therapeutic window of eligibility while waiting in the diagnostic queue.

Furthermore, PET scans cost between $3,000 and $8,000, require exposure to ionizing radiation, and are largely concentrated in affluent urban centers. Lumbar punctures, while highly accurate, are invasive, painful, and widely resisted by patients. A reliable, scalable, and non-invasive blood test is the only way to unclog this pipeline.

##### The Deep Tech: Immunoprecipitation Mass Spectrometry (IP-LC-MS/MS)
To understand why PrecivityAD2 succeeded where previous blood tests fell short, one must look at the analytical chemistry. Standard clinical blood tests rely on immunoassays (like ELISA or Single Molecule Array [Simoa] platforms). While immunoassays are highly sensitive and cheap, they run into severe limitations when measuring low-abundance brain proteins in plasma.

Plasma concentrations of amyloid-beta (Aβ) and tau are in the picogram-per-milliliter range—roughly 100-fold lower than their concentrations in CSF. In blood, these proteins are prone to matrix interference from high-abundance plasma proteins (like albumin), heterophilic antibodies, and cross-reactivity with non-specific peptide fragments. This is particularly problematic in patients with comorbidities like chronic kidney disease (CKD), which impairs biomarker clearance and alters absolute blood concentration.

C2N Diagnostics bypassed these limitations by using a platform developed by its scientific co-founders, Drs. Randall Bateman and David Holtzman of Washington University School of Medicine: Immunoprecipitation Liquid Chromatography-Tandem Mass Spectrometry (IP-LC-MS/MS). 

1. **Immunoprecipitation (IP):** High-affinity monoclonal antibodies are introduced to the plasma sample to specifically capture and enrich the target Aβ and tau peptides, washing away the complex plasma matrix.
2. **Liquid Chromatography (LC):** The enriched peptides are injected into a chromatography column, separating them based on their physical and chemical properties (like hydrophobicity and retention time).
3. **Tandem Mass Spectrometry (MS/MS):** Inside the mass spectrometer, the separated peptides are ionized. In the first quadrupole (Q1), ions are filtered based on their precise mass-to-charge (m/z) ratios. In the collision cell (Q2), they are fragmented, and in the third quadrupole (Q3), specific daughter fragment ions are quantified using Multiple Reaction Monitoring (MRM).

This method provides absolute molecular specificity. It differentiates phosphorylated tau-217 (p-tau217) from non-phosphorylated tau-217 (np-tau217) by detecting the exact mass shift caused by the addition of a single phosphate group (+79.98 Da) on the Threonine 217 amino acid residue, completely avoiding the antibody cross-reactivity that plagues traditional immunoassays.

##### Deciphering the Math: The APS2 Algorithm
Rather than relying on a single biomarker, PrecivityAD2 combines two independent ratios to generate a single, unified metric: the Amyloid Probability Score 2 (APS2), a value ranging from 0 to 100. The two components are:
* **The Aβ42/Aβ40 Ratio:** As amyloid plaques form in the brain, Aβ42 is sequestered out of circulation, leading to a decrease in the plasma Aβ42/Aβ40 ratio.
* **The %p-tau217 Ratio:** The ratio of p-tau217 to the sum of p-tau217 and np-tau217. Phosphorylation of tau at Thr217 is highly specific to the onset of amyloid plaque accumulation.

By using *ratios* rather than absolute concentrations, C2N’s algorithm normalizes individual physiological variations. For example, a patient with impaired renal clearance will have elevated absolute levels of both p-tau217 and np-tau217, but their relative ratio (%p-tau217) remains stable, reflecting actual brain pathology.

In a landmark clinical validation study of 1,142 individuals, the APS2 algorithm demonstrated outstanding statistical performance:
* **Area Under the Receiver Operating Characteristic Curve (AUC-ROC):** 0.94 - 0.95
* **Overall Diagnostic Accuracy:** ~91%
* **Sensitivity:** ~90%
* **Specificity:** ~92%
* **Positive Predictive Value (PPV):** 97.6%
* **Negative Predictive Value (NPV):** 93.1%

A PPV of 97.6% is clinically vital. Subjecting a patient to mAb therapy based on a false positive is not just financially wasteful; it exposes them to Amyloid-Related Imaging Abnormalities (ARIA), which can cause brain swelling (ARIA-E) or microhemorrhages (ARIA-H). The high NPV of 93.1% allows clinicians to confidently rule out Alzheimer's in patients whose cognitive decline stems from other causes.

##### EHR Plumbing and Automated Clinical Triage
The ultimate goal of this blood test is not just diagnostic accuracy, but operational integration. Healthcare systems are deploying EHR-integrated clinical decision support (CDS) tools within Epic and Cerner to automate the triage workflow.

For example, clinical initiatives like Vanderbilt Health's AI Triage Agent are showing how automated workflows handle cognitive care. When a primary care physician (PCP) enters a referral for cognitive decline, an AI middleware tool parses the patient's record, identifies the cognitive complaint, and automatically prompts the physician to order a PrecivityAD2 test. 

Once C2N processes the blood sample and returns the APS2 to the EHR, the system automatically triages the patient:
* **APS2 > 50 (High Amyloid Probability):** The EHR triggers an expedited, high-priority referral slot with a cognitive neurologist for mAb evaluation.
* **APS2 < 50 (Low Amyloid Probability):** The patient is routed away from the scarce neurology slots and kept in primary care or redirected to pathways evaluating vascular dementia, depression, sleep apnea, or metabolic deficiencies.

This automated triage reduces waitlists in specialized neurology clinics by up to 80%, filtering out patients who do not have the target amyloid pathology before they ever consume specialist resources.

##### The Economic Debate: Reimbursement and the Access Gap
While the science of PrecivityAD2 is widely praised, its economic rollout highlights deep disparities in the US healthcare system. The list price of the test is approximately $1,250. 

For years, blood-based Alzheimer's tests were classified as experimental, forcing patients to pay out-of-pocket (though C2N offers a sliding-scale financial assistance program reducing costs to $50–$1,750 based on income). This changed on July 9, 2026, when C2N announced that Anthem Blue Cross and Blue Shield will become the first major commercial insurer to formally cover the PrecivityAD2 test under a medical policy, effective October 1, 2026.

However, Medicare—which covers the vast majority of the over-65 population at risk for Alzheimer's—still lacks a National Coverage Determination (NCD) for mass-spectrometry blood diagnostics. 

This creates a highly unequal diagnostic environment: affluent seniors or those on commercial insurance get rapid blood-based triage and immediate access to mAbs, while lower-income Medicare beneficiaries must wait up to a year for a covered PET scan or undergo an invasive lumbar puncture.

##### Accelerating Clinical Trials: The Computational Drug Discovery Pipeline
Beyond clinical triage, PrecivityAD2 is transforming drug development. In traditional Alzheimer's trials, screening patients using amyloid PET has a screen-failure rate of 50% to 70%. Researchers spend millions on PET scans for patients who ultimately do not qualify.

By utilizing PrecivityAD2 as a pre-screening filter, clinical trial sponsors can identify high-probability candidates before sending them for confirmatory imaging. This drops the screen-failure rate at the PET stage to under 10%, cutting recruitment costs in half and accelerating trial enrollment timelines by over 50%. Remote sampling methods, such as those validated in the AlzMatch pilot study, and digital recruitment partnerships (e.g., C2N and Splash Clinical) are enabling global, decentralized trial designs.

##### Expert Perspectives from Silicon Valley and Beyond
The tech and biotech communities have closely tracked this shift. 

Dr. Eric Topol, founder and director of the Scripps Research Translational Institute, has frequently highlighted the potential of plasma p-tau217, writing:
> "The FDA clearance of PrecivityAD2 is a watershed moment. p-tau217 is essentially the LDL cholesterol of neurodegeneration. We finally have a highly scalable, mass-spec-validated blood biomarker that can predict and monitor Alzheimer's pathology years before clinical symptoms manifest."

Vijay Pande, General Partner at Andreessen Horowitz (a16z), sees this as a broader shift toward quantitative medicine:
> "Diagnostics is transitioning from analog, subjective, symptom-based triage to digital, high-throughput molecular diagnostics. By running high-res mass spectrometry on blood, C2N is showing how we scale specialized clinical medicine using deep tech. The next step is embedding these algorithms directly into EHR-driven triage."

Laura Deming, founder of The Longevity Fund, emphasizes the implications for preventive therapy:
> "Early detection is everything in longevity biotech. If we can run a simple, scalable blood test to identify pathology 10 years before cognitive decline, we unlock the door for prevention trials that actually work, rather than trying to salvage a dying brain."

Meanwhile, discussions on platforms like Reddit's r/medicine and X.com reflect the operational frustrations of clinicians:
> "It's insane that we have a 91% accurate Mass Spec blood test cleared by the FDA, but seniors on Medicare still have to pay $1,250 out-of-pocket or wait 9 months for a PET scan. The diagnostic bottleneck in American healthcare isn't a science problem; it's a reimbursement and software-plumbing problem."

Ultimately, PrecivityAD2 has proven the clinical validity of blood-based mass spectrometry. The technology is here, and it works. Now, the battle shifts to the clinical plumbing: integrating these metrics into automated clinical pathways and securing the reimbursement policies needed to make early detection universal.

---

### 4. Highlight

#### 4.1 Key Questions
1. How does PrecivityAD2 overcome the high analytical noise and low concentration of brain biomarkers in human plasma compared to standard immunoassays?
2. What are the operational and economic implications of using mass spectrometry-based blood tests as gatekeepers for disease-modifying Alzheimer's therapies like Leqembi and Kisunla?
3. How are healthcare systems integrating blood biomarkers into Electronic Health Records (EHR) to automate patient triage and relieve specialist bottlenecks?

#### 4.2 Highlight Text
The FDA's clearance of C2N Diagnostics' PrecivityAD2® test represents a massive leap for clinical diagnostics. By employing high-resolution mass spectrometry (IP-LC-MS/MS) rather than error-prone immunoassays, the test measures plasma Aβ42/Aβ40 and %p-tau217 ratios with ~91% accuracy compared to amyloid PET scans. Generating an Amyloid Probability Score (APS2), PrecivityAD2 acts as a non-invasive gatekeeper for newly approved disease-modifying therapies (Leqembi, Kisunla). Integrating this test into EHR systems via automated clinical triage promises to reduce specialist neurology waitlists by 80% and accelerate clinical trial enrollment, yet reimbursement gaps for Medicare patients remain a major hurdle.

#### 4.3 Hashtags
#Alzheimers #MassSpectrometry #Biotech #HealthTech #DigitalHealth
