# **T+37 Seconds: How Vulcan Centaur’s Avionics Survived a Solid Rocket Nozzle Blowout—and What It Means for National Security Space Launch**

###

At 7:25 a.m. EDT on October 4, 2024, United Launch Alliance’s (ULA) Vulcan Centaur lifted off from Space Launch Complex 41 at Cape Canaveral on Cert-2—the decisive flight required by the U.S. Space Force to certify the new heavy-lift rocket for the National Security Space Launch (NSSL) Phase 2 program. Thirty-seven seconds into flight, as the booster approached the sound barrier and the severe aerodynamic stresses of Max-Q, tracking cameras broadcast a jarring sequence: a sudden flare of orange fire, an expanding halo of sparkling debris, and a glowing ring separating from the starboard booster and tumbling into the Atlantic.

One of the vehicle’s two Northrop Grumman GEM 63XL solid rocket boosters (SRBs) had experienced an in-flight structural failure, shedding its composite nozzle extension mid-burn. 

In the unforgiving physics of rocket ascent, asymmetric failure of a solid motor during maximum dynamic pressure is historically catastrophic. The sudden, off-axis thrust deficit creates violent yaw and pitch moments capable of structural break-up or triggering an automated flight termination system (FTS) charge. 

Yet Vulcan did not disintegrate. In milliseconds, the flight control system commanded the dual Blue Origin BE-4 liquid methane engines to gimbal aggressively, counteracting the asymmetric yaw torque. Autonomous closed-loop guidance recalculated the vehicle’s energy state, burning the core stage and then commanding the Centaur V upper stage to extend its burn duration by approximately 20 seconds. Vulcan delivered its inert mass simulator into a precise target orbit.

On the launch webcast, ULA President and CEO Tory Bruno famously downplayed the failure as an *"observation on SRB No. 1."* While Bruno later took to X to laud the vehicle’s resilience—stating that Vulcan's propulsion margins *"ate the deficit for lunch"* to execute a *"bullseye insertion"*—the mishap triggered an exhaustive joint anomaly investigation by the Space Force and the FAA, uncovering crucial lessons in aerothermal engineering, flight control margins, and sovereign launch strategy.

```
                      VULCAN CERT-2 TIMELINE (OCT 4, 2024)
  T+00s                T+37s                 T+110s           T+300s              T+800s
┌───────┐         ┌─────────────┐       ┌─────────────┐   ┌────────────┐   ┌─────────────────┐
│Liftoff│ ──────> │SRB 1 Nozzle │ ────> │SRB Burnout  │──>│BE-4 MECO & │──>│Centaur V Burns  │
│SLC-41 │         │Disintegrates│       │& Separation │   │Stage Sep   │   │+20s for Bullseye│
└───────┘         └─────────────┘       └─────────────┘   └────────────┘   └─────────────────┘
                         │
                         ▼
             [BE-4 Gimbal Authority Counters
              Off-Axis Yaw/Pitch Torque Instantly]
```

#### 1. The Materials Science Breakdown: Anatomy of a GEM 63XL Failure
The GEM 63XL is a monolithic, 63-inch-diameter, 22-meter-long solid motor loaded with hydroxyl-terminated polybutadiene (HTPB) composite propellant, generating 460,000 pounds of thrust. Unlike liquid-propellant rocket engines, where turbopump throttles and propellant shutoff valves provide dynamic control, a solid motor is an unthrottleable pressure vessel operating at internal pressures well above 1,000 psi.

The nozzle assembly must survive exhaust gas temperatures exceeding 3,000°C laden with abrasive aluminum oxide particles. It relies on a multi-layered ablative defense:
* A dense **carbon-phenolic or 3D carbon-carbon throat insert** to withstand extreme thermal erosion.
* An internal **elastomeric insulator** (typically ethylene propylene diene monomer, or EPDM) bonded between the carbon-phenolic liner and the outer shell.
* A high-strength **carbon-fiber composite structural overwrap shell**.

Investigation findings revealed that the root cause was a **manufacturing defect in an internal insulator component bonded to the interior of the nozzle shell**. 

Under flight pressure and heat, hot combustion gases penetrated a bond-line flaw in the insulator. Once gas slipped behind the heat shield, it torched the structural composite overwrap. Deprived of mechanical support, the aft divergent exit cone delaminated and blew out into the slipstream at T+37 seconds.

Crucially, the booster's main pressure vessel remained intact. The motor continued to burn its remaining propellant grain until nominal burnout. However, losing the divergent section of the de Laval nozzle drastically degraded the expansion ratio ($A_e / A_t$). Without efficient supersonic gas expansion, the motor’s specific impulse ($I_{sp}$) collapsed, resulting in a sudden, sharp thrust loss.

#### 2. Flight Dynamics & Energy Margins: Why Vulcan Didn't Tumble
When the starboard booster lost thrust, Vulcan was subjected to severe destabilizing moments:
$$\tau_{\text{yaw}} \approx (F_{\text{nominal}} - F_{\text{degraded}}) \times r_{\text{arm}}$$

With one motor producing full thrust and the other heavily throttled by nozzle loss, this asymmetrical force generated an immense yaw moment threatening to pitch the vehicle into crosswinds at near-sonic velocity.

Vulcan survived due to three architectural redundancies:

1. **High-Authority BE-4 Thrust Vector Control (TVC):** The core stage is powered by two Blue Origin BE-4 engines burning liquefied natural gas (methane) and liquid oxygen, generating 1.1 million pounds of combined thrust. The BE-4s feature hydraulic gimbal actuators capable of rapid multi-degree deflections. Telemetry indicates the flight computer immediately commanded the BE-4s to vector their thrust off-center, countering the booster's asymmetric moment and holding the vehicle within tight angle-of-attack ($\alpha$) constraints.
2. **Autonomous Closed-Loop Guidance:** Vulcan does not fly a rigid, pre-programmed open-loop flight path. Its guidance computer continually calculates vehicle state vectors (position, velocity, mass) and solves real-time calculus-of-variations equations (similar to Powered Explicit Guidance, or PEG). Detecting a mounting velocity deficit, the guidance system flattened the ascent trajectory to minimize gravity losses.
3. **Centaur V’s Hydrolox Energy Reserves:** At stage separation, Vulcan was moving significantly slower than planned. The burden of orbital insertion shifted entirely to the Centaur V upper stage. Powered by two Aerojet Rocketdyne RL10C-1-1 engines with an industry-leading specific impulse (~453.8 s), Centaur V held substantial propellant reserves. The flight computer burned the RL10s for approximately **20 seconds longer** than nominal, expending reserve propellant to compensate for the first-stage deficit and achieving a flawless orbital insertion.

```
       AERODYNAMIC & THRUST FORCES DURING THE ANOMALY (T+37s)
       
                    ▲ Velocity Vector
                    │
               ┌────┴────┐
               │ Vulcan  │
               │ Centaur │
               │  Core   │
               └────┬────┘
                    │
         ┌──────────┼──────────┐
         │          │          │
    [SRB #1]      [BE-4]    [SRB #2]
 (Nozzle Loss)   (Gimbal)   (Nominal)
  Thrust: ~60%    Thrust:    Thrust: 100%
      │           Vectored       │
      ▼              ▲           ▼
   Degraded          │        460,000 lbf
                      \ 
                       \---> Gimbal Offset generates 
                             counter-torque to cancel yaw
```

#### 3. Silicon Valley & Aerospace Debates: Software Heroism vs. Hardware Fragility
The anomaly ignited instant analysis across tech and aerospace circles, contrasting the brilliance of autonomous flight control with the unforgiving realities of propulsion manufacturing.

Aerospace analyst and orbital mechanics educator **Scott Manley** highlighted the vehicle's flight dynamics in a widely viewed technical breakdown:
> *"Normally, when a solid rocket motor has a burn-through or loses a nozzle, it becomes a bomb or spins wildly out of control. Here, the BE-4 engines had enough gimbal authority to fight the asymmetric thrust vector, and the guidance software recalculated burn time in real time. The GEM 63XL runs hotter and with higher mechanical stress than the heritage GEM 63 on Atlas V, testing the physical limits of composite nozzle structures."*

Ars Technica Senior Space Editor **Eric Berger** captured the strategic dilemma facing military planners:
> *"The fact that Vulcan survived losing a nozzle without losing vehicle control or disintegrating is an extraordinary demonstration of modern flight avionics and thrust-vectoring authority. But for the Space Force, a booster shedding its nozzle mid-flight is about as bad an 'observation' as you can get on a certification flight."*

In engineering forums on Reddit (`/r/space` and `/r/ula`), senior aerospace engineers debated the risk profile of high-energy composite motors:
> *"Vulcan's control architecture did exactly what modern safety-critical software is designed to do: absorb physical component degradation and execute mission objectives. But you cannot use software margins to subsidize hardware defects. If an insulator delamination occurs closer to the casing joint or triggers uneven burnback, no TVC gimbal angle in the world can save the vehicle."*

#### 4. The Geopolitical Stakes: The Pentagon’s Dual-Sourcing Imperative
Cert-2 was the final technical hurdle standing between ULA and operational certification under the Pentagon's **National Security Space Launch (NSSL) Phase 2** contract. Under the Phase 2 allocation, ULA secured 60% of high-priority national security launches, with SpaceX receiving 40%. 

The strategic doctrine behind this split is **Assured Access to Space (A2S)**. By congressional mandate, the Department of Defense refuses to depend on a single launch provider—no matter how reliable. With SpaceX launching Falcon 9 rockets every few days, the commercial launch market has become a de facto monopoly. If a generic turbopump flaw or upper-stage relight failure grounds the Falcon fleet, America’s access to orbit closes overnight.

The Vulcan Cert-2 anomaly created a severe operational bottleneck:
* **Payload Manifest Backlog:** Critical national reconnaissance assets, including **USSF-106** (carrying the Air Force Research Laboratory’s experimental Navigation Technology Satellite-3, or NTS-3) and **USSF-87**, were queued directly behind Cert-2.
* **Supply-Chain Scrutiny:** Space Systems Command demanded full destructive testing and pedigree verification across Northrop Grumman's motor casting and nozzle lay-up lines in Promontory, Utah, before clearing flight hardware.
* **Cadence Pressure:** With Amazon’s Project Kuiper demanding dozens of Vulcan launches alongside national security obligations, ULA faces relentless pressure to ramp production from a handful of launches a year to over twenty.

#### The Verdict
Vulcan Cert-2 will be remembered as a landmark case study in modern autonomous aerospace engineering: a vehicle that suffered an acute propulsion failure at trans-sonic speed, dynamically restructured its flight profile, and fulfilled its mission. 

Yet in national security launch operations, margin is meant to absorb unpredictable atmospheric winds and thermal variations—not manufacturing defects. Until Northrop Grumman proves that its composite bonding process can match the perfection of Vulcan’s flight software, the Pentagon’s quest for a resilient dual-source launch architecture remains hanging on the line.

---

# 4. Highlight

### 4.1 Key Questions
1. How did Vulcan Centaur survive an in-flight solid rocket booster nozzle blowout at Mach 1 without disintegrating?
2. What specific materials science defect in Northrop Grumman's GEM 63XL motor caused the nozzle liberation?
3. Why does this anomaly threaten the U.S. Space Force’s strategic push to break SpaceX's launch monopoly?

### 4.2 Highlight Text
Thirty-seven seconds into Vulcan Centaur’s Cert-2 flight, an unexpected mechanical failure struck: a Northrop Grumman GEM 63XL solid rocket booster shed its composite nozzle mid-ascent. While such a failure typically destroys a launch vehicle, Vulcan’s avionics reacted instantly. Dual Blue Origin BE-4 engines gimbaled to counteract massive yaw torque, while Centaur V extended its burn by ~20 seconds to deliver the payload into its target orbit. But despite this triumph of autonomous flight software, the hardware failure triggered intense scrutiny—delaying critical Space Force missions and testing America’s sovereign dual-launch strategy.

### 4.3 Hashtags
#VulcanCentaur #SpaceForce #AerospaceEngineering #SpaceX #ULA
