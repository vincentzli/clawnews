# **Silicon in the Void: Google’s Project Suncatcher, Trillium TPUs in LEO, and the Physics of Orbital AI Compute**

---

####

On October 1, 2026, when SpaceX’s Falcon 9 launches from Space Launch Complex 4E at Vandenberg Space Force Base on the Transporter-18 rideshare mission, it will carry an experimental payload that could redefine the long-range architecture of machine learning infrastructure: the **MVP** prototype satellite for **Project Suncatcher**.

Developed through a joint initiative between Google Research, Google Cloud, and Planet Labs, the mission aims to test high-density enterprise AI silicon in Low Earth Orbit (LEO). By embedding Google’s flagship Trillium (TPU v6e) accelerator into a custom-engineered Planet satellite bus, Suncatcher evaluates whether the next frontier of hyper-scale AI computing belongs in space.

The strategic catalyst behind Project Suncatcher is a structural crisis in terrestrial utility grids. Across the United States, data center interconnection queues at regional transmission operators—such as PJM Interconnection, Dominion Energy in Virginia, and ERCOT in Texas—now routinely average five to seven years. As gigawatt-scale data center proposals strain regional energy infrastructure, tech giants face escalating power prices, cooling water restrictions, and carbon footprint scrutiny.

"If AI is a foundational general-purpose technology, demand for AI compute—and energy—will continue to grow," observes **Blaise Agüera y Arcas**, Vice President, Fellow, and CTO of Technology and Society at Google, who co-authored the foundational Suncatcher system design paper (*arXiv:2511.19468*) with Google Senior Vice President **James Manyika**. "The Sun is by far the largest energy source in our solar system, emitting $3.86 \times 10^{26}\text{ W}$—more than 100 trillion times humanity's total electricity production. In a dawn-dusk sun-synchronous orbit, solar panels receive up to eight times more annual energy than on Earth, free from atmospheric absorption and the day-night cycle."

Yet escaping terrestrial grid congestion forces computer architects to confront the brutal physics of orbital spaceflight: radiative thermal dissipation, cosmic radiation, and formation-flight orbital dynamics.

```
+-------------------------------------------------------------------------+
|                       PROJECT SUNCATCHER MVP BUS                        |
|                                                                         |
|  [ Ultra-Thin Deployable Solar Wings: Dawn-Dusk Sun-Tracking AM0 ]      |
|                                |                                        |
|                                v                                        |
|  +-------------------------------------------------------------------+  |
|  | GaN Core Regulators (Fast Latch-up Crowbar & Rail Isolation)       |  |
|  +-------------------------------------------------------------------+  |
|                                |                                        |
|                                v                                        |
|  +-------------------------------------------------------------------+  |
|  | GOOGLE TRILLIUM TPU v6e ACCELERATOR                               |  |
|  |  * Dual Matrix Multiply Units (MXU)  * HBM Subsystems (ECC Scrub) |  |
|  |  * SDC-Hardened Logic Pipeline       * PCIe Gen 5 Host Bridge     |  |
|  +-------------------------------------------------------------------+  |
|                                |                                        |
|            [ Conductive Heat Pipes / Vapor Chamber ]                    |
|                                |                                        |
|                                v                                        |
|  +-------------------------------------------------------------------+  |
|  | Latent Heat Thermal Capacitor (Paraffin/Metallic PCM Matrix)      |  |
|  +-------------------------------------------------------------------+  |
|                                |                                        |
|                                v                                        |
|  [ High-Emissivity Shaded Radiator Panel: Radiative Stefan-Boltzmann ]  |
+-------------------------------------------------------------------------+
```

---

### The Satellite Bus: Integrating Trillium Silicon

The core computing payload of the MVP satellite is a commercial-grade Google Trillium TPU v6e accelerator paired with an AMD host subsystem. Operating high-density silicon in orbit required Planet Labs to overhaul its standard satellite bus.

As **Will Marshall**, Co-Founder and CEO of Planet Labs, articulated on *Freakonomics Radio* (Episode 682, "Should A.I. Move to Space?"):
> *"The space industry is shifting from launch-constrained to compute-constrained. For decades, the entire challenge was getting mass into orbit. Now, with falling launch costs, the primary challenge is operating high-performance silicon per watt within orbital constraints."*

To survive the physical stresses of spaceflight, the Trillium module is isolated via titanium damping mounts to attenuate launch acoustic vibration. Electrically, high-efficiency Gallium Nitride (GaN) power stages convert power directly from the solar array bus down to sub-1.0V core rail voltages, engineered to handle sudden load swings without destabilizing the bus.

---

### Vacuum Thermodynamics: The Stefan-Boltzmann Constraint

Thermal management is the most severe physical hurdle for space-based computing. On Earth, high-performance data centers rely on forced air or liquid cooling loops to dump heat into the atmosphere. In the hard vacuum of LEO ($10^{-7}\text{ to }10^{-9}\text{ Torr}$), conduction and convection do not operate. All thermal energy must be dissipated via radiation governed by the **Stefan-Boltzmann law**:

$$q = \epsilon \sigma A \left( T_{\text{radiator}}^4 - T_{\text{sink}}^4 \right)$$

Where:
* $\sigma = 5.670374 \times 10^{-8}\text{ W}/(\text{m}^2\cdot\text{K}^4)$
* $\epsilon$ is the radiator's surface emissivity ($\approx 0.88–0.92$ using optical solar reflectors)
* $A$ is the radiating surface area ($\text{m}^2$)
* $T_{\text{radiator}}$ is the radiator temperature in Kelvin
* $T_{\text{sink}}$ is the effective sink temperature of space

For silicon to remain reliable, die temperatures must generally remain below $85^\circ\text{C}$ (358 K). Factoring in thermal interface material (TIM) resistance and heat-pipe temperature drops, the maximum radiator temperature is bounded around $T_{\text{rad}} \approx 60^\circ\text{C}$ (333 K). 

While ideal deep space radiates toward $\approx 3\text{ K}$, a satellite at 650 km in LEO is exposed to an Earth infrared emission flux of $\approx 237\text{ W/m}^2$, plus reflected solar albedo. Consequently, the net radiative rejection capacity drops to just **$250–350\text{ W/m}^2$**. At this rate, continuously dissipating a multi-kilowatt server node would require an impractically large radiator array, creating severe aerodynamic drag and structural mass penalties.

#### The 15-Minute Pulsed Compute Architecture
To solve this, Google and Planet introduced a **pulsed duty-cycle architecture**. The Trillium TPU runs high-intensity inference workloads in short bursts of approximately **15 minutes**. 

Thermal energy generated during these bursts is routed via oscillating heat pipes into a **Phase-Change Material (PCM) thermal capacitor** integrated within the chassis. By absorbing heat through latent heat of fusion (melting a paraffin or metallic alloy matrix), the PCM buffers the thermal spike and keeps the die junction safely below $80^\circ\text{C}$. Once the 15-minute compute window concludes, the TPU throttles to an idle state, allowing the thermal capacitor to slowly radiate its stored energy into space over the remaining 75 minutes of the 95-minute orbit.

---

### Radiation Hardening: Cyclotron Testing at UC Davis

Low Earth Orbit exposes commercial electronics to cosmic rays, solar proton events, and trapped radiation in the South Atlantic Anomaly. Rather than building an expensive, custom radiation-hardened-by-design (RHBD) chip from scratch, Google sought to characterize standard COTS Trillium silicon.

At the **UC Davis Crocker Nuclear Laboratory**, researchers exposed the Trillium v6e to a 67 MeV proton beam generated by a 76-inch cyclotron, with beam intensities ranging from 2 pA (~2 rad/min) to 1 nA (1 krad/min).

```
+-------------------------------------------------------------------------------+
|             TRILLIUM TPU v6e RADIATION TOLERANCE (UC DAVIS CROCKER LAB)       |
+------------------------------------+------------------------------------------+
| Parameter                          | Empirical Finding                        |
+------------------------------------+------------------------------------------+
| Total Ionizing Dose (TID) Hard Stop| No hard failures observed up to 15 krad  |
| Mission TID Life Requirement       | ~750 rad (5-yr LEO life @ 150 rad/yr)    |
| High Bandwidth Memory (HBM) Margin | Irregularities emerge at >2 krad         |
| Silent Data Corruption (SDC) Rate  | 1 event per 14.4 to 20 rad               |
| Inference SDC Error Probability    | ~1 error per 3,000,000 inferences        |
| Single Event Functional Interrupt  | ~1 event per 5 krad                      |
| Single Event Latch-Up (SEL) Status | Mitigated via microsecond crowbar clamp  |
+------------------------------------+------------------------------------------+
```

Key empirical findings include:
1. **Total Ionizing Dose (TID):** At 650 km dawn-dusk LEO with 10 mm Al equivalent shielding, expected radiation is ~150 rad(Si)/year (~750 rad over a 5-year mission). The Trillium TPU survived up to **15 krad(Si)** with **zero hard failures**, demonstrating substantial TID margin.
2. **High Bandwidth Memory (HBM) Vulnerability:** The HBM subsystem showed test irregularities above **2 krad(Si)**, establishing memory degradation as the primary lifespan limit.
3. **Single-Event Effects & SDC:** Single Event Upsets in logic and SRAM produced Silent Data Corruption (SDC) at an average rate of one event per 14.4 to 20 rad. For transformer models, this translates to roughly **one error per 3 million inferences**. 

While acceptable for inference, this SDC rate would corrupt multi-week foundation model training runs without system-level interventions:
* **Microsecond Crowbar Latch-Up Circuits:** High-speed current-sense amplifiers monitor core power rails to detect Single-Event Latch-Up (SEL) events, triggering a solid-state crowbar circuit to power-cycle rails within microseconds before destructive thermal runaway occurs.
* **Continuous Memory Scrubbing:** On-chip SRAM and HBM deploy aggressive SECDED ECC alongside firmware-driven background scrubbing to eliminate single-bit errors before multi-bit flips accumulate.
* **Dual-Modular Redundancy & Checkpointing:** Inference workloads utilize rolling state hashes and localized dual-modular redundancy (DMR) with rapid checkpoint rollbacks upon error detection.

---

### Economic Modeling: Starship and Launched Power Prices

The financial feasibility of space-based compute hinges on launch economics. Google’s researchers evaluated launch cost trajectories using **Wright’s Law**, which models cost declines against cumulative production. Analyzing SpaceX's historical launch data from Falcon 1 to Falcon Heavy demonstrates a consistent **~20% learning rate** (costs decrease by ~20% for every doubling of cumulative mass launched).

```
+-------------------------------------------------------------------------------+
|         LAUNCHED POWER PRICE COMPARISON (SUNCATCHER / ASTRONOMICS)           |
+------------------------------------+--------------------+---------------------+
| Satellite Bus / Platform           | Cost @ $3,600/kg   | Cost @ $200/kg      |
|                                    | (Falcon 9 Reused)  | (Starship Scaling)  |
+------------------------------------+--------------------+---------------------+
| Starlink v2 Mini (Optimized Proxy) | $14,700 / kW / yr  | $810 / kW / yr      |
| Starlink v1                        | $26,600 / kW / yr  | $1,470 / kW / yr    |
| OneWeb Bus                         | $135,800 / kW / yr | $7,500 / kW / yr    |
| Iridium NEXT                       | $124,600 / kW / yr | $6,900 / kW / yr    |
+------------------------------------+--------------------+---------------------+
| Terrestrial U.S. Data Centers      | $570 – $3,000 / kW / yr (PUE 1.1 - 1.4)  |
+------------------------------------+--------------------+---------------------+
```

At current Falcon 9 commercial pricing (~$3,600/kg), launching a satellite with Starlink v2 mini-class metrics costs approximately **$14,700/kW/year** (amortized over a 5-year lifecycle)—far too expensive compared to U.S. data center power spend of $570 to $3,000/kW/year.

However, if high-flight-rate reusable heavy-lift vehicles such as Starship push launch prices down to **$200/kg**, the launched power price drops to **$810/kW/year**. At that price, orbital solar power reaches economic parity with terrestrial electricity bills.

"Reaching sub-$200 per kilogram is the critical economic threshold," explained **Travis Beals**, Project Suncatcher Lead at Google, during the *Freakonomics Radio* discussion. "Matching a single 1-gigawatt terrestrial data center would require roughly 10,000 satellites generating 100 kW each. When ground facilities face five-year grid delays, orbital deployment scales purely on manufacturing throughput."

---

### 2027 Roadmap: Optical Meshes and 81-Satellite Clusters

The October 1 launch focuses primarily on single-satellite thermal and radiation baselines. Google has already planned a 2027 follow-up mission deploying two satellites to test high-bandwidth **Optical Inter-Satellite Links (OISL)**.

While standard commercial satellite laser cross-links operate at 10 to 100 Gbps across thousands of kilometers, TPU clusters require multi-terabit bandwidth for Inter-Chip Interconnects (ICI). Google’s architectural solution relies on **dense formation flight**.

Google modeled an **81-satellite cluster** flying in an elliptical formation within a 1 km radius at 650 km altitude.

```
                    ORBITAL INTER-CHIP FABRIC (81-SAT CLUSTER)
                    
                   [Sat 02] <======= 10 Tbps OISL ======> [Sat 03]
                      ^ \                                   / ^
                      |   \                               /   |
                      |     \                           /     |
                   10 Tbps   10 Tbps             10 Tbps   10 Tbps
                      |         \                     /       |
                      |           v                 v         |
                   [Sat 01] <=====> [REFERENCE SAT S0] <===> [Sat 04]
                      |           ^                 ^         |
                      |         /                     \       |
                   10 Tbps   10 Tbps             10 Tbps   10 Tbps
                      |     /                           \     |
                      v   /                               \   v
                   [Sat 08] <======= 10 Tbps OISL ======> [Sat 05]
```

Because received optical power follows the Friis transmission formula:

$$P_R = P_T \cdot G_T \cdot G_R \cdot \left(\frac{\lambda}{4\pi d}\right)^2 \cdot L_{\text{other}}$$

Received power scales inversely with the square of the distance ($P_R \propto 1/d^2$). Compressing inter-satellite spacing from 5,000 km to **under 1 km** increases optical power density by over six orders of magnitude. 

This enables satellites to use COTS Dense Wavelength Division Multiplexing (DWDM) coherent transceivers with PM-16QAM modulation over the C-band. In bench-scale tests, Google demonstrated **800 Gbps unidirectional (1.6 Tbps bidirectional)** throughput across free-space links. With spatial multiplexing across a 10 cm aperture, aggregate bandwidth reaches **9.6 to 12.8 Tbps**, effectively reproducing terrestrial datacenter pod fabrics in orbit.

Using Hill-Clohessy-Wiltshire equations accounting for Earth's $J_2$ oblateness, relative cluster drift can be maintained with under 3 m/s per year of delta-v station-keeping.

---

### Moonshot or Practical Future?

The engineering community remains divided on orbital compute. On r/hardware and X, skeptics highlight unaddressed maintenance challenges: on Earth, failed components are hot-swapped within minutes, whereas orbital hardware failures permanently degrade cluster capacity. Ground-to-orbit downlink bottlenecks also remain significant, as cloud cover and short pass windows constrain optical communication downlinks.

Proponents counter that terrestrial energy limits will force radical architectural shifts. As Dylan Patel of SemiAnalysis pointed out on X:
> *"When regional utilities tell hyperscalers that new 500MW substation builds won't be energized until 2031 or 2032, deploying modular compute clusters in orbit stops looking like pure science fiction and starts looking like enterprise risk hedging."*

The October 1 launch of the MVP satellite aboard Transporter-18 will deliver the first empirical telemetry on high-performance TPU operation in space. Whether orbital AI compute becomes mainstream infrastructure or remains an exotic experiment, Google and Planet are actively validating whether silicon in the void can break through Earth's energy ceiling.

---

### 4. Highlight

#### 4.1 Key Questions
1. **Can commercial AI accelerators survive orbital radiation?**
   Google’s cyclotron tests at UC Davis show the Trillium TPU v6e withstands up to 15 krad(Si) Total Ionizing Dose with zero hard failures—far exceeding the ~750 rad 5-year LEO requirement—while soft error rates (~1 per 3M inferences) remain manageable for inference via ECC and checkpointing.
2. **How does an orbital data center dissipate heat in a vacuum?**
   Lacking convective cooling, heat rejection relies on Stefan-Boltzmann radiation ($250–350\text{ W/m}^2$ net in LEO). The MVP satellite uses a 15-minute pulsed compute duty cycle with phase-change material (PCM) thermal buffering to absorb heat spikes and dissipate them during idle orbital windows.
3. **When does space-based compute become economically viable?**
   Under Wright’s Law, if heavy-lift reusable rockets like Starship reduce launch costs to ~$200/kg, the launched power price falls to ~$810/kW/year, achieving parity with terrestrial data center power expenditures ($570–$3,000/kW/year).

#### 4.2 Highlight Text
On October 1, 2026, Google and Planet Labs will launch the "MVP" prototype satellite aboard SpaceX’s Falcon 9 Transporter-18, testing commercial Google Trillium TPUs in low Earth orbit for Project Suncatcher. Aiming to bypass multi-gigawatt terrestrial grid backlogs, the mission tests key off-Earth engineering solutions: a 15-minute pulsed compute duty cycle with phase-change thermal buffering to counter vacuum heat limits, latch-up protection circuits against cosmic radiation, and short-range (<1 km) multi-terabit optical cross-links. If launch costs hit $200/kg, orbital AI could reach parity with terrestrial power economics.

#### 4.3 Hashtags
#ProjectSuncatcher #OrbitalCompute #GoogleCloud #TPU #SpaceTech #AIHardware #SpaceX
