# **Figure AI Inks $6B Mega-Deal for 100,000 NVIDIA Vera Rubin GPUs: Inside Brett Adcock’s Hyperscale Gamble to Solve Physical AI**

###

The debate over the true bottleneck of humanoid robotics has long divided Silicon Valley into two dogmatic camps. On one side stand classical roboticists and mechanical engineers who argue that the physical world is an unforgiving domain of non-linear contact dynamics, thermal dissipation, gear backlash, and custom actuator physics. On the other side stand the extreme compute maximalists who argue that mechanics are a solved commodity—and that general-purpose physical intelligence is purely a function of multimodal token throughput, model parameter capacity, and brute-force scaling.

Figure AI has just placed the largest financial bet in robotics history on the latter thesis.

In a multi-year strategic partnership with hyperscale AI cloud provider Nscale, Figure has committed an initial $3.5 billion—with contractual provisions scaling beyond $6 billion—to secure an unprecedented compute footprint of up to 100,000 NVIDIA GPUs built on the next-generation **NVIDIA Vera Rubin** architecture. The deployment, scheduled to break ground at Nscale’s hyper-dense data center facility in Barstow, Texas, in the second half of 2027, marks a seismic shift in how embodied artificial intelligence is funded, architected, and trained.

Under the terms of the agreement, Nscale becomes Figure’s preferred cloud infrastructure provider while taking an equity stake in the humanoid robotics startup. Concurrently, Figure’s autonomous bipedal units are slated to be deployed directly into Nscale’s supply chain operations to assist in the mechanical assembly, rack servicing, and physical logistics of the very GPU clusters training them.

"We are largely constrained by data and compute needed to train Helix, our physical AI model for humanoid robotics," Figure CEO Brett Adcock declared when announcing the transaction. "This partnership provides the compute runway to scale Helix and unlock human-level dexterity and physical intelligence."

NVIDIA founder and CEO Jensen Huang immediately hailed the arrangement as the definitive realization of his long-prophesied industrial loop: "This partnership represents the activation of the robotics flywheel: training Figure’s models on NVIDIA Vera Rubin via Nscale’s cloud, validating them in NVIDIA Isaac Sim, and deploying them onto Figure’s robots powered by onboard NVIDIA silicon."

Yet beneath the eye-watering capital expenditure lies an intense technical controversy. Can an exaflop-scale cluster of Vera Rubin GPUs bridge the infamous "sim-to-real" chasm, or is Figure attempting to brute-force a physical reality that cannot be conquered by autoregressive transformers and synthetic domain randomization alone?

---

### Dissecting Brett Adcock’s Thesis: Actuator Mechanics vs. Token Throughput

For decades, the failure modes of humanoid robotics were attributed to mechanical deficiencies: insufficient power-to-weight ratios in brushless DC (BLDC) motors, excessive backlash in cycloidal or harmonic strain wave gearboxes, poor compliance in series-elastic actuators (SEAs), and thermal throttling under sustained torque loads.

Adcock’s foundational bet with Figure 02 and the forthcoming Figure 03 is that mechanical hardware has reached a sufficient threshold of dynamic performance. With custom integrated cycloidal actuators delivering torque densities north of 150 Nm/kg, 16-degree-of-freedom dexterous hands equipped with integrated load cells, and sub-millimeter position encoders, the physical platform is no longer the rate-limiting step.

Instead, Adcock posits that humanoid capability scaling is bounded by an information-theoretic bottleneck: **multimodal token throughput per second during pre-training and real-time inference frequency at the edge.**

```
[ Traditional Robotics Paradigm ]
Sensory Feed -> Kinematic State Estimator -> Non-linear MPC / QP Solver -> Trajectory Execution (Classical PID)
   * Fragile, environment-specific, high engineering overhead, zero cross-task generalization.

[ Foundation Physical AI Paradigm (Helix) ]
Multi-Camera RGB-D + Proprioception + Tactile Grid -> High-Bandwidth VLA Transformer -> Action Space (Continuous Torques/Deltas)
   * Scales monotonically with compute (Flops) and action tokens, generalizable across embodiments.
```

In large language models (LLMs), an autoregressive model processes discrete scalar tokens at roughly 30 to 100 tokens per second. In contrast, an embodied Vision-Language-Action (VLA) foundation model operates under severe continuous multi-stream constraints:
1. **Multi-Camera Visual Streams:** 4 to 6 synchronized RGB-D streams at 1080p, running at 30–60 Hz (~1.2 GB/s raw sensory ingest).
2. **Proprioceptive Joint State:** Joint positions, angular velocities, motor bus currents, and torque feedback from 40+ degrees of freedom at 200 Hz to 1 kHz.
3. **High-Density Tactile Matrices:** Sub-millimeter pressure, shear, and micro-slip tactile sensors on every fingertip and palm surface, sampled at 100 Hz.
4. **Action Prediction Space:** Continuous 6-DoF end-effector trajectory deltas, gripper grasp forces, and full-body whole-body control (WBC) joint torques, inferred with sub-20ms closed-loop latency.

When formulated as a unified token sequence, training a physical foundation model to master long-horizon manipulation and robust bipedal locomotion across millions of edge cases requires petabytes of synchronized multimodal tokens per training epoch. Without massive compute clusters capable of sustaining hundreds of exaflops of low-precision floating-point arithmetic, training runs stall on context windows and parameter scaling.

---

### The 'Helix' Technical Pipeline: High-Frequency VLA and End-to-End Tactile Fusion

At the center of Figure’s scaling roadmap is **Helix**, the company’s proprietary Vision-Language-Action foundation model.

```
+---------------------------------------------------------------------------------------------------+
|                                 HELIX FOUNDATION ARCHITECTURE                                      |
+---------------------------------------------------------------------------------------------------+
|  [Multi-Camera RGB-D Video]      [Natural Language Goals]       [High-Density Tactile Arrays]     |
|             |                               |                                 |                   |
|             v                               v                                 v                   |
|  Spatial-Temporal Vision Encoder     Task Tokenizer             Continuous Haptic Transformer     |
|             |                               |                                 |                   |
|             +-------------------------------+---------------------------------+                   |
|                                             |                                                     |
|                                             v                                                     |
|                     +-----------------------------------------------+                             |
|                     |     Low-Frequency Semantic Trunk (5-10 Hz)    |                             |
|                     |   Long-Horizon Reasoning & Affordance Parsing |                             |
|                     +-----------------------------------------------+                             |
|                                             | Latent Task Embedding                               |
|                                             v                                                     |
|                     +-----------------------------------------------+                             |
|                     |   High-Frequency Action Diffusion/Flow Head   | <--- Proprioception (500Hz) |
|                     |        Continuous Motor Control (50-200 Hz)   |                             |
|                     +-----------------------------------------------+                             |
|                                             |                                                     |
|                                             v                                                     |
|                        Joint Position / Velocity / Torque Targets                                 |
+---------------------------------------------------------------------------------------------------+
```

Helix departs from earlier decoupled architectures—where a vision-language model (VLM) emitted discrete high-level text commands to a separate classical trajectory planner—in favor of a tightly coupled, hierarchical physical transformer:

1. **Dual-Frequency Hierarchical Decoupling:**
   * **The Semantic Reasoning Trunk (5–10 Hz):** A multi-billion parameter autoregressive transformer that consumes tokenized video frames and semantic natural language prompts to perform scene decomposition, affordance mapping, and dynamic object tracking.
   * **The Action Flow Matching Head (50–200 Hz):** A low-latency generative diffusion or flow-matching action head conditioned on the latent embeddings of the semantic trunk. This head ingests real-time high-frequency proprioception (joint positions, IMU linear accelerations) and outputs continuous chunked motor actions over a receding horizon.

2. **End-to-End Tactile Sensory Integration:**
   One of the primary failure modes of existing VLA models is their over-reliance on visual feedback. In contact-rich physical tasks—such as insertion, wire harness routing, or grasping slick deformable objects—the end-effector occludes the target object precisely at the moment of contact. Helix addresses this via a specialized continuous haptic transformer layer that processes high-resolution pressure matrices. Latent tactile tokens are cross-attended directly with the action head, enabling reflex-level grip-force stabilization in under 10 milliseconds without round-tripping through the higher-level vision encoder.

3. **Cross-Embodiment Sim-to-Real Pre-Training:**
   Figure trains Helix using unified coordinate frameworks across heterogeneous physical embodiments. By normalizing kinematic trees and actuator torque limits into a shared latent action space, Helix is pre-trained not only on Figure 02 and 03 teleoperation data, but across tens of thousands of simulated robot arms (UR5, Franka Research 3) and dual-arm manipulation platforms.

---

### Jensen Huang’s 'Robotics Flywheel' on the Vera Rubin Architecture

The deployment of 100,000 GPUs at Nscale’s Barstow facility represents the first hyperscale implementation of NVIDIA’s complete physical AI software and hardware stack:

```
[ Nscale Barstow Datacenter: 100k Vera Rubin GPUs ]
        |
        |--- Pre-Training: Helix Foundation VLA Model (FP4 / FP8 Tensor Cores)
        |--- Simulation: NVIDIA Isaac Sim / Isaac Lab (Omniverse PhysX 5)
        |       * Millions of parallel environments
        |       * Extreme domain randomization (friction, mass, sensor noise)
        v
[ Model Quantization & Compilation: TensorRT-LLM / TensorRT Edge ]
        v
[ Onboard Embedded Silicon (NVIDIA Jetson/Drive Thor SoC) ]
        |
        |--- Edge Inference: Sub-20ms Action Generation (<150W Thermal Envelope)
        |--- Edge Failure Logging -> Real-World Fleet Telemetry
        v
[ Telemetry & Figure 'Index' Human-in-the-Loop Data Collection ]
        |
        +---- Re-ingested into Nscale Compute Cluster (Flywheel Loop Closes)
```

#### The Hardware: NVIDIA Vera Rubin Platform
Slated for general data center ramp in 2026–2027, the Vera Rubin architecture replaces the Blackwell generation:
* **Vera CPU:** Custom high-IPC Arm-based processor designed to eliminate pipeline stalls when feeding high-velocity multimodal video and sensor queues into GPU memory.
* **Rubin GPU:** Equipped with next-generation **HBM4** high-bandwidth memory delivering in excess of 10 TB/s memory bandwidth per package, alongside native sub-8-bit microscopic precision data formats (FP4 and NVFP4).
* **NVLink 6:** Provides up to 3.6 TB/s of bidirectional interconnect bandwidth per GPU, allowing massive model-parallel and tensor-parallel sharding of multi-hundred-billion-parameter VLA networks across liquid-cooled supercomputing pods.

#### The Simulation Engine: Massive Isaac Lab Domain Randomization
Training purely on real-world teleoperation data is computationally and logistically non-viable. Figure leverages NVIDIA Isaac Sim and Isaac Lab to run millions of parallel simulation instances across tens of thousands of Rubin GPUs.

To overcome the sim-to-real gap, the pipeline executes **extreme domain randomization**:
* **Physics & Dynamics Perturbation:** Randomizing static and dynamic friction coefficients ($\mu \in [0.1, 1.8]$), restitution, mass distributions, center of gravity offsets, and actuator backlash matrices.
* **Photorealistic Visual Randomization:** Modulating lighting conditions, ray-traced reflections, camera intrinsics, lens distortions, motion blur, and ambient occlusion using NVIDIA Omniverse RTX rendering.
* **Latency Injection:** Simulating jitter, packet drops, and sensor latency (10–50ms) across the control loop to ensure policies remain robust against onboard hardware interrupts.

#### Edge Quantization and Low-Power Execution
A 100-billion-parameter foundation model cannot run uncompressed on a bipedal robot operating within a 150-watt to 250-watt thermal envelope. The final stage of the flywheel requires compiling the Helix action policy through NVIDIA TensorRT, quantizing weights from FP8 down to FP4. The quantized low-level action head is executed directly on Figure’s onboard dual-SoC compute architecture (such as NVIDIA Jetson Thor or Drive Thor), delivering 50 Hz closed-loop control without relying on cloud connectivity.

---

### The Great Debate: Brute-Force Compute vs. The Physical Contact Data Wall

Despite the momentum of the Figure-Nscale partnership, the global robotics community is deeply divided over whether brute-force compute can truly solve physical intelligence.

#### The "Compute & Sim Scaling" Maximalists
Proponents of the Figure approach argue that robotics is simply experiencing its "Sutton’s Bitter Lesson" moment—the historical reality that methods relying on human domain expertise and hand-crafted heuristics are inevitably crushed by general methods leveraging raw computation.

Dr. Jim Fan, Senior Research Scientist and Head of the GEAR (Generalist Embodied Agent Research) team at NVIDIA, has consistently advocated this thesis on X (formerly Twitter):
> *"The foundation model of robotics cannot be built purely on physical robot hours. Physical teleoperation does not scale to billions of tokens. The only path to general-purpose embodied AI is massive, parallelized simulation (millions of physics steps per second) combined with internet-scale passive video pre-training. Once a model understands intuitive 3D physics and visual semantics from web-scale data, a modest amount of embodied grounding is all that's required."*

Josh Payne, CEO of Nscale, doubled down on this perspective during the announcement:
> *"Physical intelligence is the ultimate frontier of AI. Just as we saw compute scaling unlock reasoning in LLMs, we are about to see exaflop-scale compute unlock physical dexterity in humanoids. Figure has the hardware and the vision; Nscale is providing the planetary-scale infrastructure engine."*

#### The "Data Wall & Contact Dynamics" Skeptics
Conversely, prominent AI scientists and veteran roboticists warn that physical interaction contains non-linearities that internet video and synthetic simulation cannot resolve.

Yann LeCun, Chief AI Scientist at Meta and pioneer of deep learning, has repeatedly challenged the application of autoregressive VLA architectures to physical control:
> *"Autoregressive prediction of actions in continuous physical spaces is fundamentally unsuited for real-world robotics. The real world is continuous, partially observable, and fraught with micro-uncertainties. Generating motor actions token by token leads to compounding errors and catastrophic drift. Unless your model possesses an explicit, non-generative Joint Embedding Predictive Architecture (JEPA) world model, throwing 100,000 GPUs at autoregressive token generation is just burning cash against a conceptual brick wall."*

Rodney Brooks, roboticist, co-founder of iRobot and Rethink Robotics, and professor emeritus at MIT, expressed characteristic skepticism regarding the timeline and reliance on simulation:
> *"Simulators are doomed to succeed. In simulation, you define the rules, and the robot learns to exploit the simulator’s mathematical approximations. But real-world contact dynamics—grease on a metal shaft, the friction of a worn gasket, thermal expansion of aluminum joints, deformable cable routing—are messy, chaotic, and non-differentiable. You cannot compute your way around the friction coefficient problem with synthetic data. Physical AI will hit a hard data wall long before it replaces a single line worker."*

Sergey Levine, Associate Professor at UC Berkeley and co-founder of Physical Intelligence (π0), also emphasizes the unique bottleneck of embodied data:
> *"The fundamental difference between language and robotics is that language is an artifact of communication, densely packed with semantic meaning, while robotics is physical interaction governed by forces. You cannot observe forces in passive YouTube videos. You can watch someone turn a bolt a million times, but the video will never tell you the peak torque required to break the thread loose. Physical AI requires rich physical action-torque data, and that data is vanishingly scarce."*

---

### Strategic Divergence: Figure AI vs. Tesla Optimus vs. Boston Dynamics

The massive capital commitment to Nscale highlights Figure’s distinct strategic posture relative to its primary rivals:

| Strategic Vector | **Figure AI** (Helix / Nscale) | **Tesla Optimus** | **Boston Dynamics** (Atlas Electric) |
| :--- | :--- | :--- | :--- |
| **Compute Sourcing** | Hyperscale Cloud Partnership (Nscale, $6B, 100k NVIDIA Vera Rubin GPUs) | In-House Vertical (Tesla Dojo + internal H100/H200/B200 clusters) | Enterprise Parent (Hyundai) + Academic Cloud Alliances |
| **Model Architecture** | End-to-End VLA Foundation Model (Helix) with dual-frequency semantic/action heads | End-to-End Deep Neural Networks derived from FSD vision-to-action pipelines | Hybrid: Model Predictive Control (MPC) + Whole-Body Control + Reinforcement Learning |
| **Data Collection Philosophy** | Synthetic Isaac Sim (mass domain randomization) + 'Index' crowdsourced physical data | Massive in-house teleoperation fleets + transfer learning from millions of Tesla vehicle video feeds | Classical dynamics modeling, trajectory optimization, targeted task-specific imitation learning |
| **Actuator Philosophy** | Commercial/Custom Cycloidal drives; standardized modular bipedal hardware | Proprietary vertically integrated custom actuators (rotary & linear), custom tactile sensors | High-power custom electric actuators, extreme dynamic range, high-torque joint modules |
| **Deployment Horizon** | Pilot industrial deployments (BMW Spartanburg, Nscale data center infrastructure) | Tesla Gigafactory manufacturing lines (internal operational deployment first) | Automotive logistics (Hyundai), industrial inspection, high-mobility dynamic manipulation |

* **Tesla’s Vertical Monolith:** Under Elon Musk, Tesla rejects third-party cloud providers, relying entirely on internal compute infrastructure. Tesla’s competitive advantage lies in its fleet data pipeline: thousands of internal teleoperators wearing custom VR and motion-capture rigs, directly mirroring the trajectory generation pipelines perfected for Full Self-Driving (FSD).
* **Boston Dynamics’ Hybrid Rigor:** Boston Dynamics continues to rely on decades of deterministic control theory. While Atlas Electric integrates learned reinforcement learning policies for locomotion over complex terrain, the core safety and balance mechanisms remain anchored in high-frequency Model Predictive Control and whole-body optimization. For Boston Dynamics, unconstrained end-to-end neural networks represent an unacceptable safety and determinism hazard in heavy industrial environments.

---

### The Verdict: Silicon Valley’s High-Stakes Gamble on Physical Reality

Figure AI’s $6 billion partnership with Nscale is more than a commercial hardware agreement; it is an audacious stress-test of the deep learning scaling hypothesis applied to physical reality.

If Brett Adcock’s thesis holds true—if high-frequency token throughput, 100,000 Rubin GPUs, and massive synthetic domain randomization can force general physical policies to emerge—Figure will have successfully cracked Moravec’s paradox, establishing the definitive operating system for humanoid labor.

If, however, physical reality refuses to be tokenized—if micro-contact dynamics, friction hysterias, and unpredictable physical interactions demand hundreds of millions of real-world physical teleoperation hours—Figure will face a punishing capital burn in the dust of Barstow, Texas.

The race for physical AI is no longer confined to the lab bench. It is now measured in megawatts, square footage, and tens of thousands of liquid-cooled Rubin GPUs.

---

## 4. Highlight

### 4.1 Key Questions
1. **The Core Scaling Bottleneck:** Is general-purpose humanoid capability bounded by multimodal token throughput and cloud compute, or will physical AI hit an insurmountable data wall without massive real-world physical teleoperation datasets?
2. **Sim-to-Real Contact Dynamics:** Can extreme domain randomization inside NVIDIA Isaac Sim and 100,000 Vera Rubin GPUs accurately model non-linear contact dynamics (friction, compliance, micro-slips) without failing in real-world deployment?
3. **Architectural Divergence:** Will Figure AI’s end-to-end VLA cloud-flywheel strategy triumph over Tesla Optimus’s vertically integrated in-house fleet data and Boston Dynamics’s hybrid classical-RL controls?

### 4.2 Highlight Text
Figure AI has locked in an unprecedented $6B multi-year deal with Nscale for 100,000 NVIDIA Vera Rubin GPUs, marking the largest compute gamble in robotics history. CEO Brett Adcock is betting that humanoid dexterity isn’t constrained by mechanical actuators, but by multimodal token throughput and compute scaling. Powering Figure's next-gen 'Helix' VLA model via Jensen Huang's 'robotics flywheel,' this Barstow, Texas deployment pits brute-force synthetic simulation against the physical contact data wall. As Yann LeCun and Rodney Brooks sound alarms over compounding autoregressive errors and sim-to-real gaps, Figure is testing whether compute alone can conquer physical reality.

### 4.3 Hashtags
#FigureAI #PhysicalAI #Robotics #NVIDIARubin #HumanoidRobots #ArtificialIntelligence #TechDeepDive
