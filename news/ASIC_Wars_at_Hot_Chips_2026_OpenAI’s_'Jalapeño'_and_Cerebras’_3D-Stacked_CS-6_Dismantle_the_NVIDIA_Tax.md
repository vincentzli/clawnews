# **ASIC Wars at Hot Chips 2026: OpenAI’s 'Jalapeño' and Cerebras’ 3D-Stacked CS-6 Dismantle the NVIDIA Tax**

##

CUPERTINO, CA — The atmosphere inside the Flint Center at Hot Chips 2026 was electric. For years, the silicon landscape has operated under a single, unchallenged premise: NVIDIA defines the ceiling of AI compute. But this year, a structural shift occurred. As frontier models like [DeepSeek R1](https://github.com/deepseek-ai/DeepSeek-R1) and OpenAI's GPT-OSS 120B shift the workload bottleneck from training to intensive, multi-step agentic inference, the industry is hitting a hard wall: memory bandwidth. 

The stars of this year's symposium—OpenAI's newly unveiled custom inference ASIC, **Jalapeño**, and Cerebras Systems’ radical **CS-6** wafer-scale roadmap—are proof that the industry is abandoning general-purpose GPUs in favor of clean-sheet, specialized silicon designed to solve the memory-bandwidth crisis.

### OpenAI's Jalapeño: The 9-Month Codex Miracle

The most anticipated disclosure came from OpenAI, which detailed its first-generation custom inference processor, Jalapeño. Developed in deep stealth with Broadcom and Celestica, Jalapeño is a 700W chip built on TSMC’s N3P process node. It features a massive **216 GB of HBM4 memory**, delivering an unprecedented **15.4 TB/s of memory bandwidth**.

```
+--------------------------------------------------------+
|                      JALAPEÑO ASIC                     |
|  TSMC N3P | 700W TDP | 216 GB HBM4 | 15.4 TB/s Bandwidth  |
+--------------------------------------------------------+
|   [ HBM4 ]       [ NUMA Spatial Compute ]       [ HBM4 ]|
|   108 GB  <=====>  216x Custom Tensor Core  <=====> 108 GB |
|  7.7 TB/s         (MXFP4/MXFP8 Native)         7.7 TB/s|
+--------------------------------------------------------+
```

What shocked the Hot Chips audience was not just the hardware specifications, but the speed of execution. OpenAI managed to go from initial RTL (Register Transfer Level) design to manufacturing tape-out in a rapid nine-month window (with a 16-month total development cycle from team assembly). This was made possible by utilizing OpenAI’s own Codex models to generate Verilog, automate layout verification, and optimize custom execution kernels. 

In public benchmarks using the *InferenceX* suite running GPT-OSS 120B and DeepSeek R1, Jalapeño demonstrated up to **1.9x higher performance-per-watt** (AI work per kilowatt) and up to **3.6x lower end-to-end latency** compared to NVIDIA’s state-of-the-art GB200 and GB300 systems. 

Dylan Patel, Chief Analyst at SemiAnalysis, commented on the breakthrough:
> "It is highly unusual for a first-generation custom ASIC to be competitive with, let alone outperform, established industry leaders like NVIDIA. The secret sauce here is extreme hardware-software co-design. When you control the model architecture, the compiler, and the silicon, you can strip away all the general-purpose overhead that plagues general-purpose GPUs."

Jalapeño achieves this by utilizing a NUMA-style spatial architecture that natively supports the Open Microscaling (MX) specifications, specifically MXFP8 and MXFP4 numerical formats. This minimizes precision requirements while maintaining model accuracy, allowing Jalapeño to run frontier models at a fraction of the memory footprint.

### Cerebras CS-6: 3D Stacking Bypasses the Memory Wall

While OpenAI is focusing on rack-scale ASIC integration, Cerebras Systems is taking wafer-scale engineering to its logical extreme. At Hot Chips, Cerebras unveiled the roadmap for its **CS-6** system. 

Historically, Cerebras’ Wafer-Scale Engine (WSE) bypassed the memory bottleneck by relying exclusively on high-speed, on-chip SRAM. This achieved petabytes-per-second of bandwidth, but limited capacity (the WSE-3 had only 44GB of SRAM). For trillion-parameter models, SRAM-only architectures required clustering multiple wafers, which introduced network latency.

The CS-6 solves this memory capacity limit by **3D-stacking DRAM directly onto the wafer-scale engine**. By using Through-Silicon Vias (TSVs) to stack DRAM dies directly on top of the logic and SRAM layers, Cerebras maintains its signature low-latency fabric locality while expanding memory capacity by orders of magnitude.

```
+------------------------------------------+
|          3D-Stacked DRAM Layers          |
+------------------------------------------+
|  ||||||  TSVs (Through-Silicon Vias)     |
+------------------------------------------+
|       Wafer-Scale Logic & SRAM (WSE)     |
+------------------------------------------+
```

Andrew Feldman, CEO of Cerebras, explained the design philosophy:
> "Traditional GPU clusters are stuck in an architectural cul-de-sac. They waste massive power and latency just moving data across boards and switches. By stacking memory directly on the wafer, we maintain the physical proximity of data to compute. Speed is the defining currency of the AI era, and infrastructure execution, not just model intelligence, will define the next phase."

### The Battleground: Prefill vs. Decode and Disaggregated Inference

The underlying theme of Hot Chips 2026 was **disaggregated inference**. Traditionally, LLM inference runs prefill (compute-bound, processing the prompt) and decode (memory-bandwidth-bound, generating tokens autoregressively) on the same chip, leading to poor hardware utilization. 

The industry is moving toward separating these workloads. Prefill is handled on compute-dense clusters, while decode is routed to memory-bandwidth-optimized hardware. 

Interestingly, OpenAI is taking a unique path with Jalapeño, opting for a three-phase execution model:
1. **Prefill Phase:** Compute-bound processing to build the Key-Value (KV) cache.
2. **Drafting Phase:** Latency-bound generation using speculative decoding.
3. **Verification Phase:** Bandwidth-bound validation of drafted tokens.

To handle the massive KV-cache transfers required for this three-phase approach, OpenAI and Celestica engineered a rack-scale pod configuration. Using Broadcom Tomahawk 6 Ethernet switches (boasting a massive 102.4 Tbps of switching capacity and up to 128 x 800GbE ports), the system scales up to 2,048 ASICs in a 16-rack pod. This allows for near-instantaneous KV-cache migration between chips, turning the rack itself into the primary unit of compute.

### Disrupting the Nvidia Monopoly

The economics of AI are at a tipping point. Operating trillion-parameter models using Nvidia’s H100 or Blackwell lines is becoming financially unsustainable for consumer scale. By bypassing Nvidia's software stack (CUDA) through their own compiler pipelines, OpenAI and Cerebras are proving that vertical integration is the only way to make agentic AI commercially viable.

Sam Altman, CEO of OpenAI, recently noted:
> "Hardware-software co-design is the only path left to make agentic compute economically viable. We cannot serve the next generation of models on general-purpose chips without breaking the bank. If we want agentic AI to be ubiquitous, we have to control the unit economics at the transistor level."

NVIDIA's moat has always been software. But when a customer only needs to run one software stack—their own—CUDA ceases to be a barrier. Jalapeño and the CS-6 prove that when software companies design their own silicon, NVIDIA's margins are the first thing to be compressed.

---

# 4. Highlight

## 4.1 Key Questions
1. How does OpenAI’s Jalapeño ASIC achieve a 3.6x latency reduction over NVIDIA Blackwell?
2. How does Cerebras CS-6 solve the wafer-scale memory capacity limit without sacrificing data locality?
3. How does disaggregated prefill/decode scheduling alter the unit economics of serving trillion-parameter agentic models?

## 4.2 Highlight Text
The silicon monopoly is cracking. At Hot Chips 2026, OpenAI debuted 'Jalapeño,' a custom 700W inference ASIC designed using Codex in just nine months. Boasting 216 GB of HBM4 and 15.4 TB/s bandwidth, Jalapeño delivers up to 1.9x better performance-per-watt than NVIDIA’s Blackwell systems. Meanwhile, Cerebras’ CS-6 roadmap bypasses the memory capacity wall by 3D-stacking DRAM directly onto its massive wafer-scale engine. As serving trillion-parameter models shifts to disaggregated, rack-scale architectures, hardware-software co-design is rewriting the economics of AI.

## 4.3 Hashtags
#HotChips2026 #OpenAIJalapeno #CerebrasCS6 #AIChips #Semiconductors
