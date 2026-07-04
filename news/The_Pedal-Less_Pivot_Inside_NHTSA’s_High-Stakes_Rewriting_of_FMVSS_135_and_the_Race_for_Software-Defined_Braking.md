# **The Pedal-Less Pivot: Inside NHTSA’s High-Stakes Rewriting of FMVSS 135 and the Race for Software-Defined Braking**

####

Silicon Valley has long treated the Federal Motor Vehicle Safety Standards (FMVSS) as the ultimate regulatory final boss. For over half a century, the code of federal regulations has dictated that if you want to put a passenger vehicle on a public road in the United States, it must have a steering wheel, a rearview mirror, and—crucially—a physical, foot-operated brake pedal. 

On June 26, 2026, the Department of Transportation’s National Highway Traffic Safety Administration (NHTSA) dropped a Notice of Proposed Rulemaking (NPRM) that fundamentally rewrites this paradigm. The proposed update to [FMVSS No. 135](https://www.federalregister.gov/documents/2026/06/26/2026-13589/federal-motor-vehicle-safety-standards-light-vehicle-brake-systems) (Light vehicle brake systems) would officially eliminate the requirement for physical, hand- or foot-operated brake controls in vehicles designed exclusively to be operated by Automated Driving Systems (ADS).

This is not a minor bureaucratic tweak. It is the administrative clearing of a multi-billion-dollar bottleneck that has held back purpose-built robotaxis for years. But beneath the regulatory relief lies a massive engineering, legal, and safety challenge: How do you validate braking reliability in a vehicle with no mechanical backups, and what happens when the safety loop is defined entirely in lines of code?

---

### The Regulatory Backdrop: Duffy’s Framework and the Death of AV STEP

To understand how we arrived here, we have to look back at the broader administrative maneuvers of the Department of Transportation under Transportation Secretary Sean Duffy. In April 2025, Duffy unveiled the administration’s Automated Vehicle (AV) Framework. The framework’s mission was clear: eliminate the regulatory "red tape" that has historically forced autonomous vehicle developers to crawl through the snail-paced "Part 555" exemption process, which caps non-compliant deployments at a meager 2,500 vehicles per manufacturer annually.

Simultaneously, NHTSA realized its previous strategy was failing. On the same day the FMVSS 135 update was proposed, NHTSA formally withdrew its January 15, 2025 NPRM for the **Automated Driving System-Equipped Vehicle Safety, Transparency, and Evaluation Program (AV STEP)**. 

AV STEP was intended to be a voluntary, data-sharing sandbox where developers could test novel vehicle designs. However, the program got caught in a crossfire. Industry players complained that its data-reporting requirements were excessively burdensome for a voluntary framework, while safety advocates and labor unions argued that a voluntary program lacked the teeth to enforce safety. 

By killing AV STEP and pushing directly for concrete updates to FMVSS 135, the DOT is pivoting from a voluntary "test-and-see" model to a permanent, performance-based regulatory standard. As Secretary Sean Duffy noted during the framework's release, *"We need national uniformity and streamlined processes to ensure American developers aren’t left behind by foreign competitors operating under more flexible rules."*

---

### The Engineering Reality: Replacing the Foot Pedal with ASIL-D Redundancy

In a traditional vehicle, FMVSS 135 compliance is tested by applying physical force to a brake pedal. The standard measures stopping distances under various conditions (cold, hot, faded, engine off) based on specific foot-pedal inputs (e.g., 6.7 to 150 lbs of force). 

For an ADS-only vehicle without a pedal, this testing methodology is completely obsolete. NHTSA’s new proposal introduces **alternative validation procedures**. Instead of relying on a human foot pushing a pedal, the agency will test the vehicle's braking systems by injecting command signals directly into the vehicle’s onboard Electronic Control Units (ECUs) based on manufacturer-provided technical specifications.

For hardware engineers, this shifts the safety burden from mechanical linkage to fully electronic, software-defined systems. In a vehicle like Tesla's Cybercab or Zoox’s carriage-style robotaxi, there is no master cylinder connected to a pedal. Instead, the architecture relies on **Brake-by-Wire (BbW)** systems.

To meet the equivalent safety levels demanded by NHTSA, these systems must achieve **ISO 26262 ASIL-D** (Automotive Safety Integrity Level D) certification. The technical breakdown of a modern ADS braking architecture typically looks like this:

1. **Dual Actuator Redundancy:** A primary electromechanical brake booster (such as Bosch’s iBooster) paired with a secondary Electronic Stability Control (ESC) unit. If the primary booster fails or loses power, the secondary unit can independently build hydraulic pressure to stop the vehicle.
2. **Dual-Wound Electric Motors:** The calipers themselves, if utilizing electromechanical braking (EMB), feature dual-wound electric motors with isolated power stages. If one set of windings shorts out, the other set provides enough torque to clamp the rotor.
3. **Isolated Power Channels:** The system must run on two completely independent electrical networks (e.g., a primary 12V/48V rail and a secondary backup battery pack) to ensure that a complete loss of main traction or auxiliary power does not disable the brakes.
4. **Communication Bus Isolation:** Under traditional setups, a single CAN bus failure could freeze commands. ADS architectures use redundant, time-triggered communication protocols (like FlexRay or Automotive Ethernet) with physical path diversity.

If a critical failure occurs, the system must trigger a "fail-operational" or "fail-safe" state, bringing the vehicle to a controlled stop, even if the primary software stack hangs.

---

### Market Impact: Waymo, Zoox, and Tesla's Cybercab

This regulatory pivot directly affects the strategic plays of the three major US robotaxi developers:

#### Waymo (The Pragmatic Hybrid)
Waymo has historically scaled its commercial operations in San Francisco, Phoenix, and Los Angeles by retrofitting conventional passenger vehicles like the Jaguar I-PACE. Because these vehicles retain traditional pedals and steering wheels, Waymo bypassed the FMVSS 135 pedal-less headache. However, Waymo’s future relies on its custom-built Geely Zeekr platform, which is designed without manual controls. The updated FMVSS 135 will allow Waymo to transition the Zeekr platform from prototype testing to mass, un-exempted commercial scale.

#### Zoox (The Custom Pod Pioneer)
Zoox has been the most aggressive defender of the purpose-built, bidirectional pod. Zoox chose to self-certify its vehicle's compliance in 2022, arguing that its redundant systems met the spirit of FMVSS. This led to intense regulatory scrutiny and a NHTSA investigation. While Zoox secured a temporary Part 555 exemption in August 2025 to run public demonstrations, the company has faced severe limits on scaling. Jesse Levinson, Zoox's co-founder and CTO, has repeatedly pointed out the absurdity of legacy rules: *"Building a car with windshield wipers and side-view mirrors that has no driver makes no sense. The regulations must match the technology."*

#### Tesla (The Cybercab Bet)
Tesla is the most volatile variable in this equation. When Elon Musk unveiled the Cybercab, the lack of a steering wheel and pedals was criticized as a regulatory non-starter. Tesla has already begun testing Cybercab prototypes in Austin, Texas, but has had to keep a safety monitor in the passenger seat. By updating FMVSS 135 to allow pedal-less operation under performance-based testing, NHTSA is handing Tesla the exact legal pathway it needs to scale the Cybercab without needing to beg for Part 555 exemptions every year. 

---

### The Legal Liability Shift: From Driver to Code

When a human driver steps on a soft brake pedal and rear-ends a truck, the liability chain is relatively straightforward: the driver is almost always at fault, with auto insurers covering the damage.

With FMVSS 135 removing the physical control, the passenger becomes a pure passenger. If a software bug or actuator failure leads to a collision, the liability shifts entirely from the "driver" (who doesn't exist) to the OEM and the ADS developer. 

On X.com, automotive legal experts have pointed out that this changes the entire underwriting model for autonomous fleets. If a vehicle has no pedals, the manufacturer cannot claim "driver interference" or "failure to take control" as a defense. The legal doctrine of *strict product liability* will apply to every incident. Underwriters will require unprecedented access to safety-critical source code, sensor logs, and hardware in-the-loop (HIL) testing data before insuring these fleets.

---

### The Battle Over Public Comments: Safety Advocates vs. Tech Optimists

With the public comment period for the FMVSS 135 NPRM open until **July 27, 2026**, the battle lines are clearly drawn.

On one side, the **Autonomous Vehicle Industry Association (AVIA)** and traditional automakers are urging NHTSA to finalize the rule swiftly. They argue that physical pedals are actually a safety hazard in an autonomous vehicle. In a vehicle with no steering wheel, a passenger could easily trip over or accidentally press a brake pedal, causing unexpected, dangerous decelerations in high-speed traffic.

On the other side, safety groups like the **Center for Auto Safety** and **Advocates for Highway and Auto Safety** are expressing deep skepticism. Their primary concern is the reliance on manufacturer self-certification and alternative testing that lacks real-world edge-case validation.

On Reddit’s r/SelfDrivingCars, one systems engineer summed up the technical anxiety: 

> *"It’s fine to remove the pedal, but what is the out-of-band backup? If the entire OS kernel panics, or if there's a localized thermal runaway in the compute rack, a human passenger has absolutely zero mechanical override to stop the vehicle. We are replacing a 100% reliable physical linkage with a complex chain of software gates. That requires a level of software auditing that NHTSA is currently not equipped to perform."*

NHTSA’s challenge over the coming months will be balancing this engineering reality with the economic pressure to unlock driverless fleets. What is clear is that the era of the mechanical brake pedal is officially drawing to a close—and the era of the software-defined stop has begun.

***

### 4. Highlight

#### 4.1 Key Questions
1. How does removing manual brake pedals impact the safety redundancy of fully autonomous vehicles?
2. What alternative validation procedures is NHTSA proposing to replace traditional foot-pedal tests?
3. How will this rulemaking shift legal liability from human drivers to autonomous vehicle developers?

#### 4.2 Highlight Text
On June 26, 2026, NHTSA proposed updating FMVSS No. 135 to eliminate physical brake pedal mandates for ADS-only vehicles, while concurrently withdrawing the AV STEP program. Led by Transportation Secretary Sean Duffy's AV Framework, this shift moves the industry from case-by-case exemptions to a standardized performance-based testing model. For developers like Waymo, Zoox, and Tesla, it removes a massive barrier to scaling purpose-built robotaxis. However, replacing mechanical backups with software-defined, ASIL-D redundant systems shifts 100% of the legal liability to OEMs, triggering intense debates on passenger overrides and software audits.

#### 4.3 Hashtags
#AutonomousVehicles #Robotics #NHTSA #TeslaCybercab #Waymo #Zoox #BrakeByWire
