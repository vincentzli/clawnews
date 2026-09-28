# **The Anatomy of a 30kg Ghost: Inside 1X’s Tendon-Driven Revolution and the High-Stakes Battle Over Domestic Teleoperation**

##

The humanoid robotics gold rush has largely converged on a singular, muscular aesthetic: rigid aluminum exoskeletons, high-ratio harmonic drives, and cycloidal gearboxes engineered to dominate automotive assembly lines. From Tesla’s Optimus to Figure AI’s Figure 02, the prevailing design philosophy treats the humanoid as a downsized, mobile machine tool—stiff, unyielding, and mechanically deterministic. 

Then came 1X Technologies’ NEO Beta. 

Unveiled by the OpenAI-backed Norwegian-American robotics firm, NEO Beta arrives not in stamped sheet metal or exposed carbon fiber, but in a padded, knit textile jumpsuit. It stands 1.65 meters (5 feet 5 inches) tall and tips the scales at an astonishingly meager 30 kilograms (66 pounds)—roughly half the mass of a 70 kg Figure 02 or a 60+ kg Tesla Optimus. Underneath its fabric skin lies an actuation architecture that radically breaks with Silicon Valley's reigning mechanical orthodoxy: a biomimetic network of high-tensile synthetic cable tendons driven by custom quasi-direct-drive (QDD) Revo1 electric motors.

Yet, as 1X prepares to insert NEO Beta into consumer living rooms for real-world testing, the technical elegance of its compliant, soft-bodied chassis is colliding with a profound sociotechnical dilemma. To navigate the infinitely chaotic edge cases of the home—from folding fitted sheets to sorting fragile dishware—1X relies on "Expert Mode": low-latency human teleoperation via VR headsets. Across X and Reddit, what 1X champions as an essential "data flywheel" has ignited fierce backlash, with critics decrying the machine as an internet-connected, panoptic surveillance proxy operated by remote gig workers inside the most private spheres of domestic life.

Here is an architectural deep dive into the mechanical physics of NEO Beta, the duality of its Redwood AI and World Model autonomy stack, and the fraught sociotechnical battleground of placing teleoperated bipedal agents inside private residences.

---

### Part I: The Mechanics of Compliance — Why 1X Eliminated Harmonic Gears

To understand NEO Beta’s 30 kg curb weight, one must understand the central mechanical bottleneck of modern humanoids: the actuator transmission.

In standard industrial robotics and contemporary humanoids like Figure 02 and Optimus Gen 2, engineers prioritize high torque density and zero backlash. They achieve this using strain wave gears (harmonic drives) or planetary gearboxes with high reduction ratios ($N \approx 50:1 \text{ to } 160:1$). While this enables rigid positional accuracy and massive joint-holding torque, it introduces an existential danger in domestic settings: **high reflected inertia**.

The reflected inertia ($J_{\text{ref}}$) perceived at an actuator's output shaft scales quadratically with the gear ratio:
$$J_{\text{ref}} = N^2 \cdot J_{\text{rotor}}$$

When a rigid humanoid swinging its arm at $1.5 \text{ m/s}$ encounters an unexpected obstacle—such as a toddler’s head or a glass coffee table—the rotor of a 100:1 harmonic gear cannot instantaneously backdrive. The joint is effectively locked during the initial milliseconds of impact. The collision force is governed by the unyielding physical inertia of the steel mechanism rather than the software control loop. To make such a robot "safe," engineers must implement active impedance control via high-bandwidth load cells and 1 kHz motor control loops. However, control loop latency (typically 1–5 ms), sensor noise, and mechanical bandwidth limits mean active safety cannot defeat the fundamental physics of high reflected inertia. If the power cuts or the loop jitters, the joint becomes a rigid, non-backdrivable lever.

```
+-----------------------------------------------------------------------------------+
|                           ACTUATION PARADIGM COMPARISON                           |
+-----------------------------------------------------------------------------------+
| Parameter               | Rigid Industrial (Figure 02 / Optimus) | Biomimetic (1X NEO Beta)        |
+-------------------------+----------------------------------------+---------------------------------+
| Primary Actuation       | High-ratio Harmonic / Cycloidal Drives | Quasi-Direct Drive (QDD Revo1)  |
| Transmission            | Rigid geared shafts at the joint       | High-tensile synthetic tendons  |
| Motor Placement         | Distal (at the elbow/wrist/knee)       | Proximal (concentrated in torso)|
| Reflected Inertia       | Massive ($J \propto N^2$, $N > 80$)    | Near-Zero ($N \le 10$)          |
| Passive Compliance      | None (mechanically stiff)              | High (intrinsic tendon elasticity)|
| Total Robot Mass        | ~60 kg to 70 kg                        | 30 kg                           |
| Kinetic Energy (at 1m/s)| ~30 J to 35 J (concentrated, hard)     | 15 J (cushioned, distributed)   |
| Exterior Shell          | Anodized aluminum / Rigid plastics     | Padded knit textile jumpsuit    |
+-----------------------------------------------------------------------------------+
```

1X founder and CEO **Bernt Øivind Børnich** rejected this paradigm entirely. NEO’s design traces its lineage to Børnich’s earlier work at Halodi Robotics with the wheeled EVE platform. Instead of heavy, high-ratio gearboxes, NEO utilizes proprietary **Revo1** electric motors—quasi-direct-drive actuators characterized by large gap diameters, high pole counts, and exceptionally low gear reduction ratios.

Because quasi-direct-drive motors produce lower torque per unit weight than highly geared motors, 1X pairs them with a biomimetic musculoskeletal transmission: **high-tensile synthetic cable tendons** (utilizing ultra-high-molecular-weight polyethylene / Dyneema fibers) routed through low-friction sheaves.

This architecture unlocks three fundamental mechanical advantages:

1. **Proximal Mass Concentration**: In rigid humanoids, motors sit directly inside the joints they articulate. Placing heavy brushless DC motors, harmonic drives, and cooling rings at the elbow, wrist, and knee dramatically increases the limb's moment of inertia:
   $$I = \sum m_i r_i^2$$
   By keeping the actuators located proximally within the torso and upper limbs, NEO routes thin tendon cables down the kinematic chain to articulate the wrists and 20+ Degree-of-Freedom (DoF) hands. This dramatically slashes distal mass, making arm swings effortless, energy-efficient, and inherently low-impact.
2. **True Passive Compliance and Backdrivability**: If an external force strikes NEO's arm, the low gear ratio allows the motor to be immediately backdriven with negligible mechanical resistance. Furthermore, the cable tendons provide intrinsic, mechanical strain compliance that absorbs shock waves at the speed of sound through the polymer fiber ($> 10,000 \text{ m/s}$), completely bypassing the latency of software control loops.
3. **Kinetic Energy Mitigation**: By paring total system mass down to 30 kg, NEO reduces the total translational kinetic energy ($E_k = \frac{1}{2} m v^2$) of a tip-over or stumble by more than 55% compared to a 70 kg competitor. Wrapped in an energy-absorbing, padded knit textile suit, the robot completely eliminates mechanical shear pinch points—a mandatory safety prerequisite for any machine sharing a floor with pets and children.

#### The Counter-Perspective: Why Competitors Call Tendons a "Mistake"
The tendon-driven paradigm is not without brutal engineering trade-offs. While 1X celebrates compliance, industrial humanoid developers view cable tendons as a maintenance and calibration liability.

Figure AI founder and CEO **Brett Adcock** has been unsparing in his critique of tendon architectures. On X and in technical interviews, Adcock candidly reflected on his company's early hardware iterations:
> *"The biggest engineering mistake we made at Figure early on was trying to build a tendon-driven hand. Tendons stretch, they creep under load, they have hysteresis, and routing cables through multiple degrees of freedom down from the forearm creates massive mechanical friction and failure points."*

Figure abandoned tendons, opting instead for custom, miniaturized direct-drive actuators embedded directly into each finger joint of the Figure 02 hand. For industrial assembly—where repetitive, sub-millimeter precision under heavy cycle counts is king—Adcock’s critique is completely justified. Cable tendons suffer from non-linear elasticity, thermal expansion, cable creep, and friction-induced backlash over millions of cycles. 

However, Børnich’s thesis is that a home is not a BMW plant. A domestic robot does not need to seat a door latch at 0.1 mm repeatability; it needs to not shatter a wine glass, crush a child’s arm, or scuff drywall when its footing slips on a rug. For 1X, mechanical compliance is not a defect—it is the foundational constraint of domestic coexistence.

---

### Part II: The Autonomy Duality — Redwood AI, World Models, and the "Expert Mode" Bridge

If NEO Beta's mechanical body is optimized for safety, its cognitive architecture is designed to confront the brutal reality of domestic autonomy: **the long tail of out-of-distribution (OOD) tasks.**

In controlled warehouse or factory logistics, the operational design domain (ODD) is constrained. A robot picks standardized bins from fixed racking. In contrast, a home presents an infinite permutation of unstructured chaos: wet laundry tangled in idiosyncratic knots, translucent glassware partially obscured by soapy water, dog toys strewn across high-pile carpets, and variable ambient lighting.

1X addresses this via a bifurcated autonomy stack:
1. **Redwood AI**: An end-to-end Vision-Language-Action (VLA) transformer model designed to unify mobile manipulation and bipedal locomotion. Redwood takes multimodal sensory inputs (onboard stereo RGB cameras, joint encoders, IMU, audio) and outputs direct motor torque or positional trajectory targets.
2. **1X World Model (1XWM)**: Pioneered under the leadership of former Google Brain roboticist and former 1X VP of AI **Eric Jang**, 1XWM is a generative, action-conditioned video world model. Rather than relying solely on classical rigid-body physics simulators (like MuJoCo or Isaac Gym), 1XWM allows the humanoid’s neural network to "mentally simulate" and predict the physical consequences of its actions before executing them in the physical world.

```
+-----------------------------------------------------------------------------------+
|                        1X NEO HYBRID AUTONOMY WORKFLOW                            |
+-----------------------------------------------------------------------------------+
|                                                                                   |
|   [Stereo RGB Cameras & Proprioception]                                           |
|                     |                                                             |
|                     v                                                             |
|          +----------------------+                                                 |
|          |  Redwood VLA Model   | <=== Generative Simulation (1X World Model)     |
|          +----------------------+                                                 |
|                     |                                                             |
|           Confidence Metric ($\sigma$)                                            |
|          /                      \                                                 |
|   High Confidence            OOD / Low Confidence ($\sigma < \tau$)               |
|         |                                 |                                       |
|         v                                 v                                       |
|  [Autonomous Execution]         [TRIGGER "EXPERT MODE"]                           |
|  - Dish sorting                 - Low-latency WebRTC Uplink                       |
|  - Fetching cups                - Remote Human Pilot (VR Headset)                 |
|  - Path navigation              - Cloud-streamed First-Person Teleoperation       |
|                                           |                                       |
|                                           +---> [Chore Completed for User]        |
|                                           +---> [Multi-modal Data Logged]         |
|                                                       |                           |
|                                                       v                           |
|                                            [Offline VLA / 1XWM Retraining]        |
+-----------------------------------------------------------------------------------+
```

#### The Flywheel: Human-in-the-Loop Teleoperation
Despite advances in generative world models, pure zero-shot end-to-end autonomous manipulation remains unsolved for domestic corner cases. 1X's strategic gambit is **"Expert Mode."**

When NEO Beta encounters a task that falls below an onboard confidence threshold—such as untangling complex laundry or navigating an unmapped clutter pattern—it initiates a low-latency WebRTC teleoperation handshake. A human operator, dubbed a "1X Expert," dons a virtual reality headset (utilizing low-latency stereo passthrough and spatial hand trackers) and assumes remote bilateral control of the robot. 

The teleoperation framework does double duty:
* **Immediate Customer Utility**: The consumer does not experience a frozen, errored robot. The chore gets completed seamlessly.
* **The "Data Engine"**: Every millisecond of the teleoperated session—RGB camera frames, depth maps, operator hand kinematics, cable tendon tension, motor currents, and tactile feedback—is compressed, encrypted, and streamed to 1X’s cloud infrastructure. This telemetry becomes ground-truth imitation learning data used to train the next iteration of the Redwood model.

Before stepping down in early 2026, **Eric Jang** frequently articulated this philosophy on X and his blog:
> *"The bottleneck to general-purpose humanoid robotics is not model capacity; it is high-quality, real-world physical interaction data. Teleoperation is not an admission of defeat—it is the ultimate data flywheel. You bootstrap utility with human intelligence while the robot's world models consume the telemetry to earn autonomy."*

NVIDIA’s Senior Research Scientist and lead of embodied AI **Jim Fan**, who has collaborated closely with 1X (demonstrating NEO running on NVIDIA’s GR00T foundation model at GTC), echoed this sentiment on X:
> *"The domestic humanoid will not be solved purely in Isaac Gym simulation. The gap between synthetic physics and the compliant dynamics of soft fabrics, deformable objects, and chaotic kitchens is too wide. The companies that deploy real hardware and build a scalable teleop-to-autonomy pipeline will capture the physical data moat."*

---

### Part III: The Domestic Surveillance Backlash — Panopticon in the Living Room

While Silicon Valley engineers celebrate the teleoperation pipeline as a masterclass in machine learning data harvesting, the public reaction outside the robotics bubble has been sharply hostile.

Following 1X’s demonstration of remote VR pilots operating NEO Beta inside domestic mockups, tech communities on Reddit (r/robotics, r/singularity, r/privacy) and X erupted in controversy. The debate shifted rapidly from kinematic compliance to constitutional and spatial privacy.

```
       "Wait... you're telling me I'm paying tens of thousands of dollars to let 
        an offshore call-center worker pilot a tele-presence camera rig into my 
        bedroom to fold my underwear?"
                               — Top upvoted comment on Reddit r/technology
```

The realization that NEO Beta is not an entirely localized, self-contained edge computer—but an embodied, bipedal tele-presence node tethered to remote human workers—has exposed significant sociotechnical fault lines.

#### 1. The Death of the Domestic Sanctuary
In Western legal tradition and global human rights frameworks, the home is afforded the highest degree of privacy protection. Smart speakers (like Amazon Echo) and robot vacuums (like Roomba) already faced severe consumer pushback over passive audio recording and floor-mapping. But a humanoid robot is structurally different: it possesses high-resolution, stereoscopic, pan-tilt head cameras, active depth sensors, microphones at human ear height, and the physical capability to open doors, manipulate drawers, and peer around corners.

Critics on X pointed out the chilling parallels to the 2022 iRobot Roomba scandal, where development-build vacuum cameras captured sensitive photos of a user on the toilet, which were subsequently sent to an overseas data-labeling vendor (Scale AI) and leaked onto private Facebook forums. 

If low-resolution vacuum cameras can cause catastrophic privacy breaches, a 1.65-meter teleoperated humanoid with dual 4K RGB feeds roaming private hallways elevates the threat surface exponentially.

#### 2. The Remote Labor Disconnect
Online discussions quickly dissected the labor economics of "Expert Mode." Tech commentators questioned the identity and vetting of the teleoperators. Will 1X deploy bonded, high-security domestic employees, or will cost pressures force the offshoring of teleoperation to Business Process Outsourcing (BPO) centers in developing nations?

On Hacker News, engineers raised acute security scenarios:
* **The "Peeping Tom" Exploit**: What prevents an operator from lingering near a master bathroom or inspecting sensitive financial documents, prescription medicine bottles, or laptop screens left on a desk?
* **Subpoenas and Law Enforcement**: Can police or intelligence agencies serve a 1X "Expert" with a warrant to passively record or inspect a private dwelling during an authorized cleaning session?
* **Ransomware and Man-in-the-Middle (MitM) Hijacking**: If the control channel between the VR headset and the robot's motor bus is compromised, an attacker gains physical agency inside a victim's house.

#### 3. The Technical Tension: Privacy vs. Teleoperation Fidelity
In response to mounting scrutiny, Bernt Børnich and 1X publicly outlined several software and hardware privacy guardrails:
* **Physical Visual Indicators**: High-visibility LED rings on NEO's "ears" and torso pulse in distinct colors when a remote human operator is actively connected.
* **Geofenced "No-Go Zones"**: Users can designate private rooms (e.g., bedrooms, bathrooms) as off-limits via a mobile app. The onboard SLAM (Simultaneous Localization and Mapping) system mechanically locks the legs and refuses traversal past virtual thresholds.
* **Edge-Based Face and PII Blurring**: Real-time segmentation networks running locally on the robot’s edge processor blur human faces, computer monitors, and text before streaming video to the cloud.

However, robotics researchers on X quickly dismantled the efficacy of edge blurring. As one prominent CV engineer noted:
> *"Real-time edge blurring creates an intractable paradox for manipulation. If the robot blurs out reflective mirrors, family photos, or cluttered papers, how does the remote operator fold laundry without knocking over an expensive vase next to it? If you aggressively blur humans to preserve dignity, the operator loses spatial awareness and risks striking a person entering the room. Privacy filters degrade the operator's situational awareness, directly degrading physical safety."*

Furthermore, Børnich’s candid acknowledgment to media outlets—that consumer data is non-negotiable for improving the system (*"If we don't have your data, we can't make the product better"*)—has reinforced fears that users are paying to become physical data mules for foundation models.

---

### Part IV: Strategic & Market Implications — The Humanoid Schism

The divergence between 1X Technologies and the rest of the humanoid pack represents a profound philosophical split in physical AI:

```
+-----------------------------------------------------------------------------------+
|                        THE DIVERGENT PATHS OF HUMANOID AI                         |
+-----------------------------------------------------------------------------------+
| Feature               | The Industrial Path (Tesla / Figure) | The Domestic Path (1X NEO)      |
+-----------------------+--------------------------------------+---------------------------------+
| Target Environment    | Structured: Factories, Warehouses    | Unstructured: Living Rooms, Homes|
| Primary Customer      | Enterprise B2B (BMW, Tier 1 Logistics)| Consumer B2C (High-Net-Worth Homes)|
| Mechanical Philosophy | Max torque, zero backlash, stiffness | Low inertia, compliance, soft-body|
| Autonomy Philosophy   | Fully autonomous or bust             | Teleop-hybrid bootstrap flywheel|
| Privacy Footprint     | Corporate IP / Factory NDA           | Intimate domestic data / GDPR   |
| Regulatory Framework  | OSHA, ISO 10218, ISO/TS 15066        | Consumer product safety, FTC, CPRA|
+-----------------------------------------------------------------------------------+
```

#### Industrial Pragmatism vs. Domestic Idealism
Tesla and Figure AI have strategically bypassed the domestic market entirely for their first commercial rollouts. Elon Musk’s Optimus and Brett Adcock’s Figure 02 are laser-focused on factory floors. In an automotive plant, workers wear steel-toed boots, the environment is mapped down to the millimeter, and a 70 kg rigid humanoid carrying a 20 kg steel stamping provides immediate, measurable ROI. Privacy is an enterprise NDA issue, not an existential consumer civil liberties debate.

1X, conversely, is attempting the hardest leap in robotics first: **the unstructured, litigious, highly intimate consumer home.**

By building a 30 kg, soft-suited, tendon-actuated machine, 1X has engineered what is arguably the most physically safe humanoid platform on Earth. A NEO falling down stairs will crack its lightweight composite shell; an Optimus falling down stairs could destroy floor joists or inflict fatal blunt trauma on a resident.

Yet, 1X's mechanical triumph has backed it into an acute sociotechnical corner. Domestic utility requires solving endless corner cases; solving corner cases currently requires human teleoperation; and human teleoperation shatters the privacy contract that protects the home. Until 1X proves that its World Models can close the autonomy loop entirely at the edge, NEO Beta will remain trapped between two worlds: a marvel of bio-inspired kinetic compliance, and the world's most intimate panopticon.

---

# 4. Highlight

## 4.1 Key Questions
1. **Can tendon-driven compliance overcome cable wear and hysteresis at consumer scale?**
2. **Will consumers accept remote human teleoperators inside their homes to fuel robotics training flywheels?**
3. **Can edge-based privacy filtering co-exist with the visual fidelity required for delicate teleoperated chores?**

## 4.2 Highlight Text
While Tesla Optimus and Figure 02 build rigid 70kg metal humanoids for car factories, 1X’s NEO Beta takes a radical detour: a 30kg, soft-knit humanoid powered by quasi-direct-drive Revo1 motors and synthetic tendons. By ditching harmonic gearboxes, 1X achieves passive mechanical compliance and eliminates crush risks. But its cognitive strategy relies on "Expert Mode"—remote VR teleoperation by human pilots to solve edge-case chores. Now, X and Reddit are erupting over domestic surveillance and data harvesting. Can 1X bridge the gap between kinetic safety and personal privacy?

## 4.3 Hashtags
#HumanoidRobotics #1XNEO #EmbodiedAI #Robotics #TechEthics #AIHardware #TeslaOptimus
