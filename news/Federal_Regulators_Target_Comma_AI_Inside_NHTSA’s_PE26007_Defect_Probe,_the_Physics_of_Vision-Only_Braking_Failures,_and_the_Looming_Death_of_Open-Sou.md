# Federal Regulators Target Comma AI: Inside NHTSA’s PE26007 Defect Probe, the Physics of Vision-Only Braking Failures, and the Looming Death of Open-Source Autonomy

On September 21, 2026, the National Highway Traffic Safety Administration’s (NHTSA) Office of Defects Investigation (ODI) dropped an unprecedented regulatory hammer that could dismantle the grassroots autonomous vehicle movement. Under docket **PE26007**, ODI initiated a formal Preliminary Evaluation into Comma AI, the San Diego-based startup founded by legendary hacker George Hotz ("geohot"). The scope is massive for an aftermarket ecosystem: an estimated 30,000 active devices across three hardware generations—the Comma Three, Comma 3X, and the recently deployed Comma Four—alongside the entire open-source openpilot software architecture.

The catalyst for PE26007 is tragic and technically specific. Federal investigators are dissecting five severe in-lane collisions where vehicles equipped with Comma hardware and running openpilot struck stationary or decelerating vehicles directly in their travel path. The toll includes three fatalities across two separate fatal crashes, alongside 11 individuals injured—several with catastrophic trauma. Crucially, ODI confirmed that Comma systems were powered on and operating in active driving automation modes during multiple of these catastrophic events.

For nearly a decade, Comma AI maintained a brilliant legal firewall, skirting motor vehicle safety regulations by selling generic "developer hardware" loaded with a bare Linux OS (AGNOS), while hosting its autonomous driving software as an open-source MIT-licensed repository on GitHub. But PE26007 obliterates that distinction. By directly scrutinizing vision-only perception limits, the unmonitored wild west of community software "forks," and aftermarket CAN bus actuation, NHTSA is setting up a landmark legal collision between federal automotive safety standards and the right to run open-source code on personal vehicles.

### I. Forensic Reconstruction: The Physics of Vision-Only Braking Failures

To understand why an openpilot-equipped vehicle could charge at full highway speeds into stopped traffic without executing emergency threshold braking, one must interrogate the underlying mathematical limitations of monocular computer vision and openpilot’s longitudinal control pipeline.

In openpilot, environment perception is centralized in `modeld`, an inference daemon running a multi-frame temporal convolutional and transformer-based neural network. The model ingests camera frames from road-facing Sony HDR image sensors (interrogating wide and telephoto fields of view) and regresses a predicted 3D path polynomial over a 10-second horizon, alongside lead-vehicle state vectors: relative distance ($d$), relative velocity ($v$), acceleration ($a$), and a detection confidence probability ($p_{lead}$).

These vision outputs pass to `plannerd`, where a Model Predictive Controller (MPC) formulates an optimal control trajectory:

$$\min_{u} \sum_{k=0}^{N} \left( w_d (d_k - d_{\text{target}, k})^2 + w_v (v_k - v_{\text{target}, k})^2 + w_a a_k^2 + w_j \dot{a}_k^2 \right)$$

This optimization problem balances following distance ($t_{gap}$) against comfort constraints on jerk ($\dot{a}$) and acceleration ($a$). 

The engineering failure occurs at the intersection of **optical flow dilation** and stationary lead detection. 

When a vehicle travels at 70 mph ($31.3\text{ m/s}$) toward a stopped car ($0\text{ m/s}$), the closing rate is high, but the visual expansion rate of the target obstacle on a 2D camera sensor is governed by:

$$\frac{\dot{\theta}}{\theta} = \frac{\Delta v}{d}$$

At a distance of 100 to 120 meters, a stationary vehicle subtends only a minimal pixel footprint. Its optical expansion rate ($\dot{\theta}$) is microscopic, blending into camera sensor noise, rolling shutter artifacts, and road vibration. Millimeter-wave radar resolves this instantly through the Doppler effect, measuring relative velocity directly from frequency phase shifts. A monocular or multi-camera vision pipeline, by contrast, must estimate depth indirectly from learned semantic priors—deducing distance from pixel dimensions and road homography.

If a stationary vehicle presents an irregular visual signature—such as a high-clearance flatbed, an asymmetric crash attenuator, heavy salt spray, or flickering emergency strobes—the neural network's detection confidence score ($p_{lead}$) degrades. Crash telemetry under federal review indicates instances of **temporal hypothesis flicker**: the model intermittently dropped lead vehicle tracking, alternating between predicting an obstacle and predicting open highway.

Because openpilot’s longitudinal planner incorporates hysteresis and low-pass filtering to protect drivers from violent false-positive "phantom braking," intermittent confidence drops cause the planner to delay or reset emergency deceleration requests. When the target’s optical expansion finally spikes—often inside $d < 35\text{ meters}$, where Time-to-Collision (TTC) is less than 1.1 seconds—the stopping distance formula dictates an impossible physical requirement:

$$a_{\text{req}} = \frac{v^2}{2d} = \frac{(31.3)^2}{2 \times 35} \approx 14.0\text{ m/s}^2 \approx 1.43g$$

Because standard automotive friction braking on dry asphalt is physically capped at roughly $0.85g\text{--}0.95g$, impact becomes physically unavoidable. Compounding this, openpilot’s safety code on the Panda microcontroller restricts maximum allowable deceleration commands sent to the vehicle's electronic brake booster, preventing maximum emergency lockup. The car strikes the stationary vehicle with devastating kinetic energy.

Former Tesla AI Director Andrej Karpathy articulated this fundamental vulnerability during his analyses of vision-only autonomy:
> *"Vision-only systems have the theoretical capacity to solve driving, but stationary obstacles at highway speeds represent the ultimate long-tail failure mode. If your temporal model flickers on object permanence for even 500 milliseconds at 70 mph, the braking envelope evaporates. Without active ranging or absolute geometric ground truth, the margin for error is zero."*

### II. Hardware vs. Software: The "Panda" Safety Enclave

Comma AI's central legal and operational defense has long rested on its hardware-software architecture. Comma Three, 3X, and Four devices ship from the factory without autonomous driving code. They arrive running **AGNOS**, a specialized, read-only Linux operating system.

The physical device connects to the host vehicle's Controller Area Network (CAN, CAN FD) via an interceptor harness spliced into the forward-facing camera or OBD-II port. Crucially, the physical link is mediated by an onboard microcontroller—the **Panda**—running open-source firmware written in MISRA-C compliant code. 

The Panda acts as an onboard safety monitor. Its firmware contains vehicle-specific safety parameters (`panda/board/safety/safety_*.h`) designed to prevent software from commanding unsafe vehicle dynamics:
* **Steering Torque Limits**: Hard clamps on maximum motor torque (`MAX_STEER`) and steering rates of change (`MAX_RATE_UP`, `MAX_RATE_DOWN`), ensuring a human driver can overpower the wheel at any time.
* **Longitudinal Acceleration Clamps**: Restricting maximum throttle voltage and deceleration commands transmitted over the CAN bus.

Under Comma’s operational model, the user mounts the hardware, powers it on, and manually inputs an installation URL (e.g., `openpilot.comma.ai`). The device pulls the openpilot codebase from GitHub, compiles the Cython and C++ daemons on device, and initializes Level 2 automated driving.

Comma AI argued this setup separated hardware sales from software deployment. In Comma's view, it was merely an electronics vendor selling a developer kit running open-source code at the user's discretion.

NHTSA's PE26007 makes it clear: regulators no longer accept this distinction.

### III. The Liability Quagmire: Community Forks and Safety Circumvention

The most legally precarious element of PE26007 is NHTSA’s formal inclusion of third-party community "forks."

Because openpilot is hosted publicly under the MIT license, an ecosystem of community modifications has flourished. Prominent community forks include **Sunnypilot** (maintained by sunnyhaibin), **FrogPilot** (maintained by FrogAi), and **Dragonpilot**. While these forks offer widespread community vehicle ports and UI refinements, they also introduce user-toggled modifications that bypass core safety limits established by upstream openpilot.

```
[ Upstream openpilot Safety Architecture ]
Camera Array -> modeld (Vision/Supercombo) -> plannerd (MPC) -> Panda (Safety Hard-Limits) -> CAN Bus
                             |
                   dmonitoringmodeld (IR Camera)
                             |
                   Strict Attention Escalation (Orange Alert -> Red Alert -> Disengage)

[ Compromised Community Fork Architecture ]
Camera Array -> modeld -------------------> Modified plannerd (Altered Jerk/Acceleration) -> CAN Bus
                                                        ^
                   dmonitoringmodeld                    |
                             |               [Dynamic Follow: t_gap clamped to < 0.9s]
              [Bypassed Driver Monitoring]              |
                             x               [Always-On Lateral: Steering persists through braking]
```

ODI investigators are focusing on three prevalent community fork modifications:

1. **Compressed Headway Distance ("Dynamic Follow")**: While upstream openpilot defaults to conservative headway gaps ($1.4\text{s}\text{--}1.8\text{s}$), community forks allow drivers to configure "aggressive" follow profiles with gaps below $0.9\text{ seconds}$, obliterating reaction buffers when lead vehicles brake abruptly.
2. **Always-On Lateral (AOL) / M.A.D.S.**: In upstream openpilot, pressing the brake pedal immediately disengages automated steering, returning 100% control to the driver. Community forks allow "Always-On Lateral," keeping automated steering engaged even while the driver manually modulates the brake, which can cause erratic vehicle dynamics during panic avoidance maneuvers.
3. **Driver Monitoring (DM) Tampering**: Upstream openpilot features an infrared cabin camera running `dmonitoringmodeld` to monitor driver eye gaze, face angle, and phone usage. If driver attention lapses, an escalation cycle triggers: audible chimes sound, and the vehicle eventually forces disengagement and slows to a stop. Several community forks and scripts allow users to extend distraction timers, silence warning chimes, or spoof driver presence signals.

In at least one fatal crash cited in PE26007, recovered device logs revealed the vehicle was running a community fork with modified driver-monitoring parameters. The driver had averted their gaze from the road for an extended period prior to the high-speed impact, entirely unimpeded by system warnings.

Dr. Missy Cummings, Director of the Mason Autonomy and Robotics Center and former Senior Safety Advisor to NHTSA, underscored the regulatory trap:
> *"The argument that a hardware manufacturer can sell an aftermarket device specifically designed to inject actuation packets onto a safety-critical vehicle CAN bus, and then wash its hands of responsibility because the consumer downloaded open-source code from a GitHub URL, is legally and technically absurd. If an aftermarket system circumvents driver monitoring and crashes into a stopped car, the entire distribution pipeline is a defect hazard under federal law."*

### IV. Ideological Standoff: Hacker Ethos vs. Federal Mandates

This confrontation has been brewing for a decade. In October 2016, NHTSA issued a Special Order to George Hotz regarding his initial "Comma One" project, warning that selling uncertified automated driving equipment violated federal safety regulations. Hotz abruptly canceled the commercial product, took to Twitter to decry regulatory overreach, and released openpilot as free software.

Hotz has long championed personal accountability over bureaucratic paternalism:
> *"openpilot is not an autonomous driving system. It is advanced cruise control. The driver is 100% in control, 100% of the time, exactly like when you turn on dumb cruise control in a 1995 Honda Civic. If you crash your car into the back of a truck, it is your fault. Do not blame the software, do not blame the tool. Personal responsibility is the only standard that scales."*

On Reddit’s **r/Comma_ai**, the community response has been defiant. Users have characterized PE26007 as regulatory capture designed to protect legacy OEMs from agile open-source competition. *"They want to outlaw open systems so automakers can lock us into monthly subscription fees for inferior driving packages,"* reads a prevailing sentiment.

However, federal statutory law stands firmly with NHTSA. Under the **National Traffic and Motor Vehicle Safety Act (49 U.S.C. § 30102(a)(8))**, the definition of "motor vehicle equipment" encompasses:

> *"...any system, part, or component of a motor vehicle as originally manufactured, or any similar part or component manufactured or sold for replacement or improvement of a system, part, or component, or as an accessory or addition to a motor vehicle."*

Because Comma AI manufactures wiring harnesses, vehicle-specific CAN gateways, and specialized compute hardware engineered specifically to take control of automotive steering and braking systems, NHTSA holds direct defect and recall authority over the company. If the agency finds that the hardware or software creates an "unreasonable risk to safety," it possesses statutory authority to order a nationwide recall under 49 U.S.C. § 30118.

### V. The Regulatory Endgame: Three Possible Outcomes

As ODI proceeds with PE26007, the investigation will determine whether to escalate to an Engineering Analysis (EA), the final precursor to a formal recall demand. Comma AI faces three potential futures:

```
[ NHTSA Investigation: PE26007 ]
                |
     +----------+----------+
     |                     |
[Outcome 1]           [Outcome 2]                [Outcome 3]
Mandatory OTA         Hardware Lockdown via      Total Recall & 
Safety Refactor       Cryptographic Signing      Commercial Ban
- Strict DM lockouts  - Locked bootloader        - Hardware declared illegal
- Severe ODD limits   - Banning community forks    aftermarket equipment
- Emulates Tesla Autopilot - End of open development - Business shuttered
```

1. **Outcome 1: The Forced OTA Compliance Update (The Tesla Autopilot Precedent)**. Emulating NHTSA’s 2023 recall of Tesla Autopilot (Recall 23V-838), regulators force Comma AI to push mandatory over-the-air updates to all internet-connected devices. This update would impose strict driver monitoring lockouts, limit operational speed envelopes, and instantly disengage if distraction exceeds two seconds. However, this remedy fails to address offline, air-gapped devices running unlinked custom forks.
2. **Outcome 2: Cryptographic Hardware Lockdown (The Death of Open Forks)**. To satisfy NHTSA that unauthorized code cannot manipulate vehicle steering and braking, regulators compel Comma AI to implement **hardware-rooted cryptographic signing**. Under this mandate, the Panda microcontroller and AGNOS bootloader would verify digital signatures before allowing code execution. Only official, safety-audited releases of openpilot signed by Comma AI would be permitted to access vehicle CAN buses. This step would insulate Comma from liability but destroy the open-source community modification ecosystem that fueled its popularity.
3. **Outcome 3: Total Recall and Commercial Invalidation**. If NHTSA concludes that aftermarket vision-only systems lacking active radar or LiDAR cannot reliably detect stationary objects at highway speeds, or that aftermarket CAN-bus command injection is inherently defective, the agency can order an outright recall of all 30,000 Comma Three, 3X, and Four devices. Comma AI would be forced to disable devices or buy them back, effectively ending open-source driver assistance in the United States.

### The Verdict

The tragedy of PE26007 is that openpilot represents a staggering technical triumph. Over hundreds of millions of real-world miles, its lateral control and vision models have frequently matched or outperformed proprietary driver-assistance systems from major automotive manufacturers.

Yet pure software brilliance cannot override the physical constraints of camera optics or the statutory realities of motor vehicle law. When high-speed vision pipelines fail to resolve stationary obstacles, and open architectures allow safety safeguards to be disabled, the boundary between open-source freedom and reckless endangerment vanishes. NHTSA’s PE26007 signals the end of the romantic era of hacker autonomy—and a sober reckoning for community-driven driving systems.

---
