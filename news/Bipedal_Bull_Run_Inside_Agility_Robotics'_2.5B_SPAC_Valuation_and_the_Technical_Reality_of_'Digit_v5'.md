# **Bipedal Bull Run: Inside Agility Robotics' $2.5B SPAC Valuation and the Technical Reality of 'Digit v5'**

###

The humanoid robotics sector just crossed its Rubicon. On July 14, 2026, Agility Robotics, the Oregon-based creator of the bipedal humanoid robot "Digit," filed a draft registration statement on Form S-4 with the SEC to merge with Churchill Capital Corp XI (NASDAQ: CCXI). The transaction values Agility at an implied pre-money equity valuation of approximately $2.5 billion and is poised to generate over $620 million in gross proceeds. This capitalization stack includes $421 million from Churchill XI’s trust and a $201 million PIPE common stock round led by Foxconn. Upon closing, the combined entity will trade under the ticker "AGLT."

The announcement has set social media ablaze, igniting fierce debates across X.com and Reddit. For skeptics, the deal smells like a rerun of the speculative 2020–2021 SPAC boom. Critics point to the wreckage of that era: Desktop Metal filed for Chapter 11 bankruptcy in July 2025; Berkshire Grey went public via SPAC at a $2.2 billion valuation, only to be taken private by SoftBank in 2023 for a mere $375 million; and Sarcos Technology was forced to abandon hardware entirely, pivoting to software under the name Palladyne AI. Bringing a pre-revenue humanoid robotics company to the public markets, they argue, offloads venture-level technology risk onto retail investors.

But supporters argue Agility is different. Unlike competitors displaying highly edited, tethered laboratory demonstrations, Agility has real, untethered hardware executing multi-hour shifts in production warehouses. 

#### **The Kinematics Feud: Digitigrade vs. Plantigrade**
The listing also marks the next chapter in a highly public, technically charged feud. In November 2025, Figure AI’s CEO Brett Adcock boasted on X that Figure 01 had been working on a BMW production line for five consecutive months, claiming Figure was "the first and maybe the only company" to achieve this. Agility Robotics quote-tweeted the post, dryly comparing Adcock's claim to someone adding lemon juice to water and claiming they invented a new drink.

Adcock fired back with a devastating prediction: Agility would be "bankrupt in <12 months," citing "poor engineering choices" and a lack of progress over the preceding decade. A VP from competitor 1X Technologies chimed in to plea for decorum ("Kindness > douchery"), while Agility replied to Adcock with a confused Ted Lasso GIF: *"Ok... guess we will go ahead and circle next November for a quick check-in."* Adcock retorted with a Sopranos meme: *"Next time you come in, you come heavy or not at all."*

Eight months later, Agility has come heavy—backed by a $620 million public market war chest. 

At the center of Adcock’s "poor engineering choices" critique is Digit's unique, bird-inspired **digitigrade leg design**. While Figure 01, Tesla Optimus, and 1X Neo mimic the human **plantigrade** (flat-footed) posture, Digit walks on its toes, using a multi-jointed leg that places its mechanical ankle high off the ground.

```
Plantigrade (e.g., Figure, Tesla)     Digitigrade (Agility Digit)
          o [Hip]                                o [Hip]
          |                                     /
          | [Knee]                             / \ [Knee/Ankle Joint]
          |                                    \
         --- [Foot]                             \ [Ankle/Foot Joint]
                                                o [Toe Contact]
```

This kinematic layout has clear engineering trade-offs:
1. **Dynamic Locomotion vs. Static Stability:** Digitigrade legs act like springs, storing and releasing mechanical energy. This makes Digit highly agile, exceptional at shock absorption, and capable of navigating stairs and cluttered aisles. However, it lacks passive stability. While a plantigrade robot can stand powered down on flat feet, Digit must constantly run active control loops, burning battery power just to stand still.
2. **Payload and Joint Torque:** Flat feet provide a broader base for lifting heavy loads. Digitigrade legs require high joint torque at the mechanical knee/ankle to support vertical payloads. Digit's payload capacity is currently capped at 35 lbs (16 kg), which some critics argue limits its utility in heavy industrial logistics.

#### **Scaling Digit v5: From Pilots to Production**
Agility plans to use the SPAC proceeds to scale production of the new **Digit v5**. This iteration features refined knee actuators, upgraded functional safety over EtherCAT (FSoE) to support Category 1 (CAT1) emergency stops, and an integrated physical AI layer to improve autonomous path planning. 

Operationally, Digit v5 is managed via **Agility Arc**, a cloud-based fleet management platform. Rather than writing custom code for every warehouse, Agility Arc integrates directly with existing Warehouse Management Systems (WMS), allowing Digit to receive tasks, recycle totes, and coordinate with Autonomous Mobile Robots (AMRs) dynamically. 

Unlike its pre-revenue SPAC predecessors, Agility claims a $300 million booked revenue pipeline, representing roughly 1,000 robots under a Robots-as-a-Service (RaaS) leasing model. Production will be anchored at its 70,000-square-foot "RoboFab" manufacturing facility in Salem, Oregon, which has a peak capacity of 10,000 robots per year.

The real test will be whether Agility can translate warehouse pilots with GXO Logistics (Spanx warehouse in Georgia) and Amazon into high-margin, scalable revenue. If Digit v5 can solve the MTBF (Mean Time Between Failures) bottlenecks that plague humanoid hardware, AGLT will be the ultimate validation of bipedal commercialization. If not, it will be the largest monument in the SPAC graveyard.

***
