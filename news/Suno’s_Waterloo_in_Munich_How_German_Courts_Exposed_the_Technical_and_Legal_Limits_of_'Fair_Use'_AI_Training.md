# **Suno’s Waterloo in Munich: How German Courts Exposed the Technical and Legal Limits of 'Fair Use' AI Training**

###

The legal fiction that artificial intelligence models merely "learn like humans" has suffered a devastating blow in Europe. On July 31, 2026, the Munich Regional Court I (Landgericht München I) ruled in favor of the German music collecting society GEMA in its high-stakes copyright infringement lawsuit against U.S.-based generative music giant Suno AI (Case ID: `42 O 763/25`). 

The court’s decision is the most technically and legally consequential ruling on AI training since the advent of generative media. By ordering Suno to cease unauthorized reproductions, disclose revenue, and pay damages, the court has effectively declared the "wild west" era of unlicensed AI training dead on European soil.

```
+---------------------------------------------------------------------------------+
|                              THE SUNO TRAINING PIPELINE                         |
|                                                                                 |
|  [Copyrighted Audio] ---> [VQ-VAE Encoder] ---> [Autoregressive Transformer]    |
|  (e.g., Alphaville)      (EnCodec/DAC Tokens)  (Learns patterns & memorizes)     |
|                                                              |                  |
|                                                              v                  |
|  [High-Fidelity Audio] <-- [Diffusion Decoder] <--- [Discrete Latent Tokens]    |
|  (Regurgitated Hook)     (Collapses into local    (Low-entropy deterministic)   |
|                           potential wells)                                      |
+---------------------------------------------------------------------------------+
```

#### Dissecting the Legal Conflict: GEMA’s Opt-Out vs. Suno’s Extraterritorial Defense
The litigation centered on six iconic pop works: Alphaville’s *"Forever Young"* and *"Big in Japan"*, Lou Bega’s *"Mambo No. 5"*, Boney M.’s *"Daddy Cool"* and *"Rasputin"*, and Helene Fischer’s *"Atemlos durch die Nacht"*. GEMA presented undeniable forensic audio evidence demonstrating that Suno's models could generate outputs that were virtually indistinguishable from the original compositions and recordings.

Suno's legal team attempted to shield its training practices under two primary frameworks: U.S. Fair Use (arguing training occurred on U.S. servers) and the EU’s Text and Data Mining (TDM) exception under Article 4 of the DSM Directive (codified in Germany as Section 44b UrhG). 

The Munich court systematically dismantled these defenses:
1. **Extraterritorial Jurisdiction:** The court ruled that German copyright law applies because Suno targets German consumers and makes the resulting infringing outputs accessible in Germany. There is no U.S.-style "Fair Use" exemption in German law.
2. **Rejection of the TDM Exception:** Under Article 4(3) of the DSM Directive, rightsholders can opt out of text and data mining if they reserve their rights in a machine-readable format. GEMA had done exactly this. The court confirmed that GEMA’s digital rights reservation was legally binding and technically sufficient, meaning Suno had no license to copy the files for training.
3. **The 'Memorization' Threshold:** Crucially, the court held that even if the TDM exception were to apply, it does not cover training that results in the model memorizing and reproducing the target works. When a model regurgitates a recognizable melody, it ceases to be "mining data" and becomes a direct instrument of copyright infringement.

#### The Technical Root Cause: Overfitting and Memorization in Generative Audio
To engineers, the court’s finding that Suno "memorized" the music is a validation of known machine learning vulnerabilities. Suno’s architecture is understood to rely on a two-step generative framework: an autoregressive transformer that operates on quantized latent tokens, and a diffusion-based decoder that converts those tokens back into high-fidelity waveforms.

```
       Loss Landscape and Manifold Collapse in Generative Audio
       
       Energy / Loss
            ^
            |       \               /       \               /
            |        \             /         \             /
            |         \           /           \           /
            |          \_________/             \_________/ 
            |          [Generalization]       [Memorization Well]
            |                                  (e.g., "Forever Young"
            |                                   due to duplication)
            |                                         |
            |                                         v
            +-------------------------------------------------------> Latent Space
```

##### 1. Autoregressive Token Lookup and Exposure Bias
Suno uses neural audio codecs (like EnCodec or Descript Audio Codec) that compress raw waveforms into discrete spatial-temporal tokens using Vector Quantization (VQ-VAE). An autoregressive transformer is then trained to predict the probability distribution of the next audio token given the history:

$$P(x_t \mid x_{<t})$$

When training datasets contain duplicated or highly similar instances of famous tracks (remixes, radio edits, YouTube stream-rips, and cover versions), the model suffers from **exposure bias**. The optimization gradient aggressively minimizes next-token prediction loss for these specific paths. During inference, when prompted with stylistic keywords matching the metadata of these tracks, the model's output entropy collapses to zero:

$$\mathcal{H}(P(x_t \mid x_{<t})) \approx 0$$

The transformer ceases to generate novel token sequences and instead acts as a deterministic lookup table, stepping through the exact token progression of the memorized song.

##### 2. Diffusion Score Collapse
To reconstruct high-fidelity audio, the latent tokens are decoded using a diffusion model (either a U-Net or a Diffusion Transformer, DiT). During training, the model learns the score function:

$$\nabla_y \log p_t(y)$$

which points toward the data manifold. If a training sample is heavily overrepresented, it creates an excessively deep local minimum—a potential well—in the loss landscape. During the reverse diffusion process, the trajectory of the latent variables is pulled into this well. Regardless of the random Gaussian noise seed $z_T$ initialized at the start of the sampling process, the path converges to the exact latent coordinates of the memorized track. When run through the decoder, it outputs the identical acoustic waveform, matching vocal timbre, specific chord progressions, and instrumental arrangements.

#### Tech Industry Backlash and Executive Debates
The ruling has ignited fierce debate across Silicon Valley. Venture capital giant Andreessen Horowitz (a16z), a major backer of generative AI startups, had previously warned the U.S. Copyright Office that imposing licensing requirements on training data would devastate the industry:

> *"The only practical way to train these models is on massive datasets that include copyrighted works. Forcing AI developers to pay licensing fees for training data will significantly disrupt the AI market, favor massive tech incumbents over startups, and harm national security."*
> — **Andreessen Horowitz (a16z) Submission to the US Copyright Office**

However, creators and technical experts argue that "fair use" was never meant to shield commercial competitors built on stolen training sets. Ed Newton-Rex, founder of the non-profit Fairly Trained and former VP of Audio at Stability AI (who resigned in protest over unlicensed training practices), hailed the Munich decision:

> *"This is a monumental victory for creators. AI music companies cannot continue training on copyrighted work without license or consent, especially when the outputs directly compete with the original artists. The court’s rejection of the TDM defense because the model 'memorizes' and reproduces the training data is legally and technically spot on. You cannot claim fair use when your model is built to replace the people it trained on."*
> — **Ed Newton-Rex, Founder of Fairly Trained**

Suno’s leadership has pushed back, defending their technology as fundamentally transformative. Suno CEO Mikey Shulman argued:

> *"Our technology does not memorize or copy music; it learns the underlying patterns of human composition to help creators make entirely new, original songs. We believe the court’s decision is based on a fundamental mischaracterization of how generative AI works, and we are evaluating all legal options, including an appeal."*
> — **Mikey Shulman, CEO of Suno AI**

#### The Global AI Training Landscape: The US-EU Schism
The Munich ruling highlights a growing divergence in the global regulation of AI training data. 

In the United States, the legal battle is framed around the four-factor fair use test. While major record labels (Sony, UMG, Warner) coordinated a massive lawsuit through the RIAA in June 2024, the outcome remains uncertain. Notably, some industry players have chosen to pivot: Warner Music Group reached a landmark partnership and settlement with Suno in November 2025, establishing an opt-in framework for artists' names, voices, and compositions. However, Sony and UMG continue to pursue active litigation, seeking massive statutory damages.

In Europe, the legal standard is far less flexible. The combination of GEMA's successful enforcement of opt-out rights under Article 4 of the DSM Directive, combined with the Munich court's strict interpretation of "memorization" as direct reproduction, means that AI developers targeting European markets can no longer rely on scraping public web data. 

AI developers are now facing a stark choice: maintain separate model weights for the European market trained exclusively on licensed, opt-in data (such as Adobe’s approach with Firefly or Fairly Trained-certified datasets), or face catastrophic liability, injunctions, and revenue disclosure orders that could render their commercial products unusable.

---

## 4. Highlight

### 4.1 Key Questions
1. **Can generative AI models be legally trained on copyrighted works in Europe without a license?**
   No. The Munich Regional Court I ruled that rightsholder opt-outs under Article 4 of the DSM Directive are legally binding, and that models which memorize and reproduce training works do not qualify for Text and Data Mining exceptions.
2. **What technical mechanism causes AI music generators to reproduce copyrighted songs?**
   Data duplication in the training set leads to exposure bias in autoregressive transformers (reducing next-token entropy to near-zero) and score collapse in diffusion decoders, pulling generative trajectories into deep potential wells that reconstruct original waveforms.
3. **How does this ruling affect the global commercial operations of AI companies?**
   AI companies face extraterritorial liability under EU laws if their outputs are accessible in Europe, forcing them to pivot away from scraped datasets toward licensed, opt-in training pipelines.

### 4.2 Highlight Text
The Munich Regional Court I’s landmark July 31, 2026, ruling in GEMA v. Suno AI has drawn a red line for generative AI. By rejecting Suno’s fair use and text-data mining defenses, the court established that models memorizing and reproducing copyrighted hits—such as Alphaville’s *"Forever Young"*—are direct instruments of infringement. Technically, this regurgitation stems from exposure bias in autoregressive transformers and score collapse in diffusion decoders, which pull generation paths into deterministic local minima. As US labels push forward with litigation, Europe’s strict licensing mandate will force AI developers to adopt opt-in, clean training datasets.

### 4.3 Hashtags
#AICopyright #GenerativeAI #MusicTech #GEMAvSuno #MachineLearning #AILaw
