# **GDDRHammer: The Physics of Charge Leakage and the End of GPU Isolation**

##

The silicon security landscape just shifted under our feet. For the better part of a decade, we viewed Rowhammer as a CPU-centric nuisance, manageable through BIOS updates and DDR4 refresh adjustments. But with the disclosure of **GDDRHammer**, the vulnerability has migrated to the high-performance world of GDDR6 memory, effectively shattering the security wall between GPUs and the host CPU.

### The Physics: Parallelized EMI
The technical breakthrough of GDDRHammer lies in its exploitation of **electromagnetic interference (EMI)** and capacitive coupling in high-density GDDR6 DRAM. Unlike standard DDR4, GDDR6 operates with significantly higher frequency and tighter refresh intervals (23ms). Conventional security wisdom suggested this would neutralize Rowhammer.

However, the researchers from the **University of Toronto (Chris S. Lin, Joyce Qu, Gururaj Saileshwar)** utilized the GPU's massive parallelism to bypass these defenses. By using CUDA to synchronize thousands of threads across multiple warps, they achieved **620,000 activations per refresh cycle**, overwhelming the in-DRAM Target Row Refresh (TRR) mitigations. This intense "hammering" causes charge leakage between adjacent capacitors, leading to deterministic bit-flips.

### The Exploit: "Memory Massaging" and Page Table Corruptions
The attack begins with the reverse-engineering of the GPU's proprietary address mapping—a "black box" typically hidden by the memory controller. Through "memory massaging," attackers can force the GPU's memory allocator to place sensitive structures, such as **GPU Page Tables**, into vulnerable DRAM rows. 

As noted by security engineer **@taviso** and discussed extensively on Reddit's *r/NetSec*, the implications are dire: by flipping a single bit in a Page Table, an unprivileged CUDA kernel can gain unauthorized access to the **host CPU's physical memory**. This allows for a full "breakout" from the GPU sandbox to the host OS.

### Impact on Cloud and AI
For Cloud Service Providers (CSPs) like **AWS** and **Azure**, the impact is immediate. In multi-tenant environments where GPUs are shared or time-sliced, an attacker can target other users' data. The research demonstrated that a single bit-flip in the exponent of a floating-point (FP16) weight can drop an AI model's accuracy from **80% to nearly 0%**.

"This is a massive blow to the 'trusted execution' model of cloud GPUs," says a lead engineer at a top-tier AI lab. "We are now looking at a performance tax—enabling System-Level ECC on NVIDIA cards—which costs us **10% in throughput**. That’s millions of dollars in compute time for a security fix."

### The Future of AI Silicon
The vulnerability is architecture-specific. While standard GDDR6 (found in RTX 3060 and A6000) is highly vulnerable, **GDDR6X**, **GDDR7**, and **HBM3** (found in H100s) utilize **on-die ECC**, which significantly raises the bar for exploitation. This discovery will likely accelerate the industry's shift away from standard GDDR6 for security-sensitive AI workloads, forcing a redesign of future AI-centric silicon to include hardware-level isolation as a first-class citizen.

---

# 4. Highlight

## 4.1 Key Questions
1. How does GDDRHammer bypass Target Row Refresh (TRR) in GDDR6?
2. Can an attacker move from an unprivileged GPU kernel to host-level root access?
3. What is the performance penalty for enabling the recommended ECC mitigations?

## 4.2 Highlight Text
The "GDDRHammer" vulnerability is the first systematic Rowhammer attack on GDDR6, weaponizing GPU parallelism to bypass hardware refresh mitigations. By achieving 620k activations/cycle—7x faster than a CPU—researchers proved that attackers can flip bits in GPU Page Tables to gain root access to host CPU memory. This breaks the security boundary in multi-tenant clouds (AWS/Azure), where a single bit-flip can also destroy AI model accuracy (80% to 0%). While H100s (HBM) remain resistant, standard GDDR6 users face a 10% "performance tax" by enabling ECC to stay secure.

## 4.3 Hashtags
#GDDRHammer #CyberSecurity #GPUComputing #AISecurity #NVIDIA #CloudSecurity
