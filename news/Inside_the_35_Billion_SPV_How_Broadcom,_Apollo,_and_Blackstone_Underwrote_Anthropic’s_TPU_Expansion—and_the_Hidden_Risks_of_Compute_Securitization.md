# **Inside the $35 Billion SPV: How Broadcom, Apollo, and Blackstone Underwrote Anthropic’s TPU Expansion—and the Hidden Risks of Compute Securitization**

##

As the race to train and deploy frontier AI models scales exponentially, a silent revolution has occurred in the financial plumbing of Silicon Valley. The era of funding massive computing clusters purely through venture capital equity rounds is dead. The capital requirements for training next-generation large language models have outgrown the risk appetite of traditional venture capital and the equity thresholds of founders. Raising tens of billions in equity means severe dilution that would strip founders of control and early investors of returns. 

Enter the landmark June 2026 transaction: a $35 billion private credit agreement orchestrated by asset management giants Apollo Global Management and Blackstone to finance Anthropic’s compute expansion. Rather than placing this hardware debt directly on Anthropic's balance sheet—a move that would degrade its financial metrics ahead of a highly anticipated IPO—the deal employs a complex, off-balance sheet Special Purpose Vehicle (SPV) structure managed by Apollo's ATLAS SP Partners. The SPV will purchase custom Google Tensor Processing Units (TPUs) and lease them back to Anthropic, securing over 1 gigawatt (GW) of compute capacity. 

But the real magic—and the systemic risk—of this deal lies in its credit enhancement. Broadcom, Google's physical co-developer and packaging partner for the TPU line, has agreed to provide "residual value guarantees" and credit endorsements for $30 billion of the senior debt tranches. This transaction marks a watershed moment where compute hardware is treated as a securitized asset class, similar to commercial aircraft fleets or real estate portfolios. However, unlike traditional infrastructure assets, AI silicon depreciates at an unprecedented rate, giving rise to the toxic threat of "compute debt."

### The Financial Architecture: Deciphering the SPV and the Three Tranches
To understand how $35 billion of institutional capital can flow to a pre-profit AI startup, one must look at the structural design of the SPV created by ATLAS SP Partners. The SPV functions as a bankruptcy-remote entity that buys the custom Google TPUs (designed in partnership with Broadcom and manufactured by TSMC) and leases them to Anthropic. 

The capitalization of the SPV is divided into distinct tranches:
* **The Equity Layer ($800 million):** Contributed directly by ATLAS SP Partners, this acts as the first-loss capital, giving Apollo de facto ownership of the vehicle.
* **Senior A1 Notes ($6 billion):** A "super-senior" tranche priced at U.S. Treasury yields plus 100 basis points. 
* **Senior A2 Notes ($24 billion):** First-lien senior notes carrying a fixed 5.75% coupon. Together with the A1 notes, this represents the $30 billion core senior debt.
* **Class B Notes ($4.5 billion):** Subordinated, second-lien notes that carry a high-yield 8.5% coupon to compensate for the lack of external credit guarantees.

The Senior A1 and A2 tranches are fully backstopped by Broadcom’s investment-grade balance sheet through a residual value support agreement. If Anthropic defaults on its lease payments, the SPV is forced to repossess and liquidate the TPUs. If the sale or re-lease of the chips fails to cover the outstanding senior debt, Broadcom is contractually obligated to pay the difference. This credit wrap effectively transfers the default risk from Anthropic to Broadcom, allowing Apollo and Blackstone to market the senior notes to conservative institutional investors like pension funds and insurance companies.

As Brad Gerstner, founder of Altimeter Capital, observed on X:
> "Traditional venture capital is simply too small to fund this scale. The transition to structured debt and private credit is the only way to fund 20-plus gigawatts of compute without destroying the equity caps of the labs."

### Broadcom’s Strategic Gambit: Securing the ASIC Pipeline
Why would Broadcom CEO Hock Tan guarantee $30 billion in debt for a third-party AI startup? The answer lies in the economics of custom silicon. 

Broadcom does not sell standard off-the-shelf GPUs. Instead, it operates as the physical design and packaging partner for Google's custom TPUs. Google designs the TPU architecture and software, while Broadcom translates those designs into silicon reality, providing high-speed SerDes IP, custom High Bandwidth Memory (HBM3e) interfaces, and advanced packaging solutions. Google is Broadcom’s largest custom silicon customer, and every TPU deployed represents highly profitable ASIC and networking revenue for Broadcom.

In April 2026, Anthropic committed to securing 3.5 GW of TPU-based AI compute from Google beginning in 2027. To satisfy this commitment, Google must procure tens of billions of dollars worth of custom TPU ASICs from Broadcom. By backstopping the SPV debt, Broadcom guarantees that the financing is approved, thereby locking in Google's TPU orders. This strategy protects Broadcom’s custom silicon pipeline and ensures it remains the dominant player in custom AI accelerators (XPUs).

Dylan Patel, Chief Analyst at SemiAnalysis, commented on the strategic alignment:
> "This is a massive coup for Broadcom. By underwriting the credit risk, they've guaranteed their own custom silicon pipeline with Google, securing billions in high-margin ASIC and networking revenue while keeping Nvidia out of Anthropic’s gigawatt-scale roadmap."

For Broadcom, this is part of a broader vision. Alongside Apollo and Blackstone, Broadcom has established the "AI XPV Platform" to deploy over 20 GW of compute capacity through 2028. As Hock Tan stated:
> "The AI XPV Platform synchronizes the world's most sophisticated capital with our hardware roadmap to enable the deployment of scale-efficient AI infrastructure with speed and certainty."

### The Obsolescence Mismatch: Why Compute Isn't Commercial Aviation
While the SPV model draws heavy comparison to aircraft leasing, the underlying physics of hardware depreciation reveal a fundamental mismatch. 

When an SPV leases a Boeing 737 to an airline, the asset has a useful life of 20 to 25 years. If the airline defaults, the plane can be repossessed and easily leased to another carrier because it is a highly standardized asset with a liquid global market. 

Contrast this with a Google TPU. A TPU has an operational shelf life of 2 to 3 years before it is rendered obsolete by rapid generational leaps (e.g., TPU v5p to TPU v6 and the upcoming TPU v7). Furthermore, TPUs are highly proprietary. They can only be hosted in Google Cloud Platform (GCP) data centers because they rely on Google's custom optical circuit switches (OCS) and proprietary networking fabrics. If Anthropic defaults, the SPV cannot repossess the TPUs and lease them to Microsoft Azure, AWS, or Meta. The secondary market for proprietary Google TPUs is virtually non-existent. Google is the sole buyer, giving it ultimate monopsony power over the repossession value.

A top engineer commented on Reddit’s r/MachineLearning:
> "If the hardware depreciates in 24 months, you aren't leasing an asset; you're taking on a massive depreciating liability disguised as project finance. If Anthropic defaults, those TPUs are paperweights to anyone but Google."

This means the "residual value" of the TPUs is close to zero outside of Google's ecosystem. Broadcom’s guarantee is not a safety net backed by physical collateral; it is a direct corporate liability.

### Systemic Risks and the "Compute Debt" Bubble
The long-term viability of debt-fueled AI infrastructure expansion hinges on a single question: Can Anthropic's model revenues grow fast enough to service the lease and interest payments?

While Anthropic's revenue is on an upward trajectory, it is dwarfed by the scale of its compute commitments. If the cost of training frontier models outpaces the enterprise demand for AI APIs, Anthropic will face a structural liquidity crisis. Under a traditional equity model, a failure to monetize means write-downs for venture capital firms—a painful but self-contained event. Under the SPV debt model, a default by Anthropic triggers structural defaults that propagate through the private credit market and onto Broadcom’s balance sheet.

If Anthropic defaults:
1. The SPV defaults on the A1, A2, and Class B notes.
2. The $4.5 billion Class B noteholders (who took on unbacked risk for an 8.5% yield) are wiped out.
3. Broadcom is forced to step in and cover the $30 billion senior debt shortfall, severely straining its cash reserves and risking a credit downgrade.
4. Private credit managers Apollo and Blackstone face massive write-offs, causing a chilling effect that would freeze AI infrastructure funding across the industry.

As Dario Amodei, CEO of Anthropic, has noted:
> "By 2026 or 2027, we will see models that cost $10 billion or even $100 billion to train. The scaling curves show no signs of flattening, and the winner will be whoever can marshal the necessary compute and power."

However, if that compute is built on a foundation of short-lived, debt-funded assets, the industry is building its scaling laws on a financial fault line. The $35 billion Anthropic deal is a masterpiece of financial engineering, but it exposes the AI ecosystem to a new kind of risk: a systemic compute debt bubble where the hardware depreciates faster than the models can monetize.

---

# 4. Highlight

## 4.1 Key Questions
1. How does the off-balance sheet SPV structure protect Anthropic's financials as it prepares for an IPO?
2. Why is Broadcom willing to backstop $30 billion of senior debt for custom AI hardware that faces a 2-3 year obsolescence cycle?
3. What are the systemic risks for the private credit market if frontier AI labs default on their hardware leases?

## 4.2 Highlight Text
Venture capital is no longer enough to fund the AI scaling wars. The landmark $35B private credit deal for Anthropic—led by Apollo, Blackstone, and Broadcom—signals a structural shift toward "compute project financing." By using an off-balance sheet SPV to lease Google TPUs, Anthropic avoids severe equity dilution. Yet, the real story is Broadcom backstopping $30B of the senior debt. While this secures Broadcom's lucrative custom ASIC pipeline, it introduces "compute debt"—a toxic mismatch where short-lived AI hardware depreciates faster than model revenues can grow, shifting default risks directly onto corporate balance sheets.

## 4.3 Hashtags
#AICapEx #PrivateCredit #Broadcom #SiliconValley #CustomASIC #TechFinance
