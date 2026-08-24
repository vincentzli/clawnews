# **Physical AI’s Billion-Dollar Concrete Reality: Inside Gravis Robotics’ $200M SoftBank Bet**

##

The venture capital world has spent the last three years funding generative AI models that write copy, generate code, and draw pictures. But in the background, a far more capital-intensive, high-stakes battle is taking shape: the struggle to automate the physical world. 

No sector represents the friction, promise, and sheer engineering complexity of this transition quite like construction. It is an industry plagued by a chronic, existential labor crisis. According to industry statistics, the U.S. construction sector alone faces a shortage of nearly 500,000 workers in 2026, with over 40% of the current workforce set to retire by 2031. Concurrently, global productivity in construction has remained stagnant for decades, lagging behind manufacturing by a factor of two.

Enter **Gravis Robotics**. The Zurich-based startup, founded in 2022 as a spin-out from ETH Zurich’s famed Robotic Systems Lab, recently announced a massive $200 million Series A funding round led by SoftBank Group. The investment values the startup at $1 billion, instantly making it Europe’s newest robotics unicorn. 

The deal is a massive validator for Gravis’ core technology: the **Gravis Rack**, a modular, rooftop-mounted hardware and software system that can retrofit standard, legacy heavy machinery—excavators, wheel loaders, and graders—and turn them into autonomous, self-operating assets. 

But as SoftBank pumps hundreds of millions into this space, it exposes a rift at the heart of industrial robotics: Should we build autonomous heavy machinery from the ground up, or is retrofitting the only commercially viable path forward?

### The Architectural Divide: Retrofit vs. Ground-Up

The core thesis behind Gravis’ strategy, shared by competitors like Built Robotics (developers of the Exosystem) and SafeAI, is that heavy machinery is already a solved mechanical problem. 

"We realized early on that heavy machinery is a solved problem mechanically," says Noah Ready-Campbell, CEO of Built Robotics. "Caterpillar and John Deere have spent a century making these steel beasts incredibly reliable. Why build a new excavator when you can just bolt on an autonomous brain?"

From a commercial perspective, retrofitting makes immense sense. Replacing a contractor’s entire fleet of excavators, which cost anywhere from $150,000 to over $1 million per unit and have operational lifespans of 10,000+ hours, represents an impossible CAPEX hurdle. Retrofitting preserves these assets, allowing operators to bolt on a system like the Gravis Rack, interface with the machine’s internal Controller Area Network (CAN) bus, and gain immediate autonomy.

However, ground-up proponents—including the research arms of major OEMs (Original Equipment Manufacturers) like Komatsu and Volvo—argue that retrofitting introduces a technological ceiling. Legacy machines are mechanically designed around human control. They feature hydraulic valves optimized for manual joysticks, operator cabs that limit sensor placement, and electrical architectures that lack the hardware-level redundancy required for true fail-safe autonomy. A ground-up autonomous excavator can dispense with the cab entirely, optimizing weight distribution, lowering the center of gravity, and natively integrating drive-by-wire hydraulic manifolds and high-bandwidth redundant wiring.

### Inside the Control Loop: Proprioception vs. Exteroception

To understand why automating an excavator is harder than automating a self-driving car, one must look at the control loop. A self-driving car primarily deals with *exteroception*—perceiving the external environment (lanes, pedestrians, signs) and navigating through it. The physical interaction with the road is mostly constant and predictable.

An excavator, however, is constantly engaged in high-force interaction with an unpredictable, subterranean medium: soil. 

"Traditional robotics relies too heavily on exteroceptive vision," explains Dr. Dominic Jud, co-founder and CTO of Gravis Robotics. "But an excavator doesn't just see the soil—it feels it. By fusing high-speed proprioceptive telemetry like hydraulic cylinder pressures and engine strain with 3D LiDAR, we bridge the physical gap where vision-only models stall."

```
                 +---------------------------------------------+
                 |               Gravis Rack                   |
                 |  - LiDAR/Cameras   - Edge Compute (Orin)    |
                 |  - RTK-GNSS        - Path Planning (SDF)    |
                 +----------------------+----------------------+
                                        | Control commands
                                        v
                 +---------------------------------------------+
                 |             Low-Level Control               |
                 |  - Electro-Proportional Valves (EPPV)       |
                 |  - CAN Bus Intercept (J1939)                |
                 +----------------------+----------------------+
                                        | Hydraulic force
                                        v
                 +---------------------------------------------+
                 |              Physical Machine               |
                 |  - Bucket Force      - Joint Displacements  |
                 |  - Soil Dynamics     - Engine RPM Strain    |
                 +----------------------+----------------------+
                                        | Proprioceptive feedback
                                        +----------------------+
```

Gravis' control architecture operates on a multi-tiered loop:

1. **Exteroceptive Mapping & Path Planning:** The Gravis Rack uses solid-state LiDARs and cameras to generate a real-time 3D Signed Distance Field (SDF) of the local terrain. The system compares this map with digital Building Information Modeling (BIM) files loaded via "The Slate" operator tablet. A high-level path planner calculates collision-free trajectories for the boom, stick, and bucket using optimized sampling-based algorithms (like RRT*).
2. **Proprioceptive Control & Force Feedback:** As the bucket enters the ground, the system encounters highly non-linear forces. To prevent the machine from stalling or tipping, Gravis implements an adaptive admittance control loop. Pressure transducers at the cylinder bores measure the exact resistance force. If the bucket hits a buried boulder, the system instantly modifies the trajectory in real-time, yielding to the obstacle rather than trying to force its way through.
3. **Sim-to-Real RL Training:** Because soil mechanics are notoriously difficult to model mathematically, Gravis utilizes Reinforcement Learning (RL). The controllers are trained in massive simulated environments using the Fundamental Equation of Earth-Moving (FEE) to model soil-tool interactions. The RL agent learns to adjust cylinder velocities based on real-time engine RPM strain and hydraulic pressure drops, mimicking the "feel" of an experienced human operator.

### Safety Challenges in Unstructured Environments

Construction sites are chaotic, highly unstructured environments characterized by shifting piles of dirt, open trenches, dynamic dust clouds, and unpredictable human workers. This poses severe challenges to robotic perception.

* **The Dust "Curtain" Effect:** Excavation generates significant airborne dust. Traditional LiDAR sensors struggle in these conditions, as the laser pulses reflect off dust particles, creating false-positive obstacles that cause the machine to halt repeatedly. Gravis mitigates this by fusing LiDAR with frequency-modulated continuous-wave (FMCW) radar, which penetrates dust clouds, and by employing software filtering algorithms that evaluate point-cloud return intensity to distinguish between solid rock and loose dust.
* **Mechanical Vibrations:** The impact forces of digging and the vibrations of diesel engines subject sensors to intense shock. This can quickly throw camera and LiDAR calibrations out of alignment. Gravis addresses this with ruggedized, dampener-mounted sensor arrays and real-time software calibration routines that use Inertial Measurement Units (IMUs) to dynamically compensate for high-frequency structural jitter.
* **SOTIF (Safety of the Intended Functionality):** Under standards like ISO 19014, systems must be safe against control system failures. But autonomous construction machinery must also account for SOTIF (Safety of the Intended Functionality)—ensuring safety when sensors and algorithms work perfectly but the AI fails to interpret an ambiguous scene (e.g., mistaking a safety vest for a warning cone under heavy shadows).

### SoftBank’s Physical AI Playbook

To understand SoftBank’s $200 million bet on Gravis, one must look at the broader strategic chess board designed by founder Masayoshi Son. Son has publicly shifted SoftBank’s vision toward Artificial Super Intelligence (ASI) operating in the physical world. 

"Physical AI is central to SoftBank's vision for the next phase of AI," says Dai Sakata, Managing Director at SoftBank Group. 

This isn't an isolated investment. In late 2025, SoftBank completed a massive $5.375 billion acquisition of Swiss industrial robotics giant ABB Robotics. By coupling ABB’s industrial footprint with its investments in Skild AI (foundational physical models), Agile Robots (under the Robo HD holding company), and now Gravis Robotics, SoftBank is assembling a full-stack monopoly on physical AI. The goal is to provide the silicon (via Arm), the foundation models, the industrial robotic arms, and the heavy-duty autonomous operating systems that will automate everything from logistics to manufacturing and infrastructure development.

### Regulatory and Liability Conflicts

Despite the influx of capital, the industry faces severe structural headwinds. 

The first is regulatory. In the U.S., the Occupational Safety and Health Administration (OSHA) operates under traditional safety standards (like 29 CFR 1926 Subpart O) that mandate qualified human operators remain at the controls of heavy machinery. There is currently no clear Federal pathway for unmanned, fully autonomous operation on open job sites. To comply, contractors must establish strict, geofenced exclusion zones, keeping humans completely separated from the autonomous machinery—a restriction that severely limits site efficiency.

The second hurdle is liability. If a 30-tonne autonomous excavator shears a high-pressure gas line, who is liable? Is it the contractor overseeing the site? The OEM who manufactured the chassis? Or Gravis, whose software planned the path? 

Because autonomous control systems must comply with rigorous functional safety standards like ISO 13849 (Performance Level d/e) and ISO 19014 (Machine Performance Level), the software must achieve a level of reliability orders of magnitude higher than standard enterprise SaaS. In the physical world, a software crash doesn't just mean a corrupted database—it means a multi-ton mechanical asset swinging out of control.

Finally, labor displacement concerns remain a friction point. The International Union of Operating Engineers (IUOE) and other labor groups argue that rapid automation threatens operator livelihoods, though tech advocates counter that automation will simply step in to fill the severe labor gap that threatens to halt infrastructure progress.

Ultimately, Gravis Robotics represents a bold bet that the future of heavy industry will not be built by wait-and-see OEMs, but by software-first startups capable of retrofitting the existing world. With $200 million in fresh capital and the backing of SoftBank's physical AI empire, Gravis is positioned to prove whether AI can master the mud.

***

# 4. Highlight

## 4.1 Key Questions
1. How does a retrofit AI system like the Gravis Rack interface with a legacy excavator's hydraulic and electronic control systems?
2. What are the key sensor limitations—specifically dust interference and high-frequency structural vibration—on dynamic construction sites?
3. How is SoftBank building a full-stack monopoly on Physical AI through its acquisitions and venture rounds?

## 4.2 Highlight Text
SoftBank’s $200M Series A in Zurich-based Gravis Robotics pushes the startup to a $1B valuation, fueling the intense debate between modular retrofitting and ground-up heavy-machinery manufacturing. While OEMs advocate for cab-less custom designs, aftermarket platforms like the "Gravis Rack" offer immediate CAPEX relief for labor-starved contractors. Gravis' secret lies in fusing exteroceptive LiDAR SLAM with proprioceptive force telemetry—essentially teaching 30-tonne excavators to "feel" the resistance of the earth via real-time hydraulic loops. With SoftBank’s $5.3B acquisition of ABB Robotics, Masayoshi Son is aggressively consolidating the physical AI value chain. 

## 4.3 Hashtags
#PhysicalAI #ConstructionRobotics #Autonomy #SoftBank #DeepTech
