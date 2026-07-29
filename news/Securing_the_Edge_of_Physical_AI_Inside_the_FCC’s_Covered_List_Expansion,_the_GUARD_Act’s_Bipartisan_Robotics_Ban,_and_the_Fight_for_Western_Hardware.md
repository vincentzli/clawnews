# **Securing the Edge of Physical AI: Inside the FCC’s Covered List Expansion, the GUARD Act’s Bipartisan Robotics Ban, and the Fight for Western Hardware Sovereignty**

##

On July 28, 2026, the U.S. Federal Communications Commission (FCC) officially expanded its "Covered List" to include foreign-produced "advanced robotic devices," targeting mobile humanoid and quadruped robots manufactured by Chinese companies. This action effectively halts the importation, certification, and commercial sale of new models of Chinese robots in the United States. While national security agencies celebrate this as a crucial step to defend critical infrastructure, the American robotics community is facing a massive crisis. U.S. universities, research institutes, and AI startups rely heavily on affordable Chinese quadrupeds, particularly those manufactured by Unitree, as standard research platforms. This ban creates a severe tension between national security and scientific innovation.

### The Policy Catalyst: The GUARD Act (H.R. 9129)
The FCC’s designation is the direct result of the **Guarding the U.S. Against Adversarial Robotics Dominance (GUARD) Act** (H.R. 9129). Introduced in June 2026 by Representatives John Moolenaar (R-MI), Jay Obernolte (R-CA), and Jennifer McClellan (D-VA), the bill mandates that national security agencies review humanoid and quadruped robots from "countries of concern." 

To bypass administrative foot-dragging, the GUARD Act built in a 365-day automatic trigger: any robotic communications equipment or service not formally cleared within one year of enactment is automatically placed on the FCC’s Covered List. Representative Moolenaar, Chairman of the House Select Committee on the CCP, has been the primary legislative driver, warning:
> *"Humanoid and quadruped robots manufactured by foreign adversaries present a severe risk of espionage and cyber warfare. These are not just toys; they are walking, sensing data-collection nodes connected directly to foreign servers."*

The interagency review process—coordinated by the Department of Homeland Security (DHS), the Department of Commerce, and the Pentagon—focused on the potential for these robots to act as "mobile Trojan horses." The resulting intelligence assessments triggered the FCC’s immediate listing.

### Technical Analysis: Vulnerability Deep-Dive
The FCC's action is backed by critical vulnerabilities uncovered by security researchers, demonstrating that these systems are highly vulnerable to local and remote exploitation:

1. **BLE Command Injection (CVE-2025-35027):** 
   Affecting the Unitree Go2, G1, H1, and B2 models, this high-severity command injection vulnerability (CVSS 7.3) resides in the Bluetooth Low Energy (BLE) Wi-Fi configuration module. When a user configures the robot’s local network credentials via the mobile app, the payload is transmitted over BLE. Attackers can inject a malicious shell command string into the SSID or password parameters. When the robot attempts to apply these settings, the system executes the commands as the `root` user via the script [wpa_supplicant_restart.sh](file:///usr/local/bin/wpa_supplicant_restart.sh). This grants the attacker a root shell on the robot's primary compute module (typically an NVIDIA Jetson Orin SoC).

2. **The CloudSail Backdoor (CVE-2025-2894):** 
   In the Unitree Go1 series, researchers exposed a persistent backdoor embedded in the integration of the CloudSail remote access service. The robot maintains a persistent WebSocket connection to external servers. An attacker possessing a valid API key can bypass local authentication entirely. This allows remote attackers to hijack the robot’s physical movement, activate the on-board camera arrays, stream live audio, and extract precise GPS/location telemetry.

3. **DDS Layer Exploitation (CVE-2026-27509 & CVE-2026-27510):** 
   The most alarming threat vector lies in the real-time communication middleware. Unitree robots utilize the Data Distribution Service (DDS) for low-latency communication between the high-level compute unit (running ROS2) and the real-time motor controllers. Because DDS traffic is unencrypted and lacks strict authentication on default Unitree setups, an attacker on the same local network can broadcast malicious DDS packets. This allows them to tamper with the mobile database or directly override the PID controller coefficients and active joint limits in the motor control loops, potentially causing violent joint over-extensions, motor burnouts, or physical collapse.

4. **Cryptographic Weakness:** 
   Analysis of Unitree’s proprietary "FMX" encryption wrapper revealed the use of static, hardcoded cryptographic keys across all shipped units. This enables any attacker with access to the firmware image to decrypt configuration files, intercept local telemetry, and reverse-engineer proprietary control algorithms.

### The FCC Covered List and Software Regulation
The FCC’s Covered List addition does not just halt physical shipments; it fundamentally alters the software lifecycle of Chinese robotic platforms:
* **No New Equipment Authorizations:** The FCC will not issue new telecommunication grants for "advanced robotic devices" from listed entities. This means new models (like the newly teased Unitree G1 humanoid iterations) cannot legally operate radios in the U.S.
* **Software Update Ban:** The FCC's definition of "covered equipment" extends to software updates and cloud-connected telemetry. Listed companies are barred from pushing firmware updates or connecting to U.S.-based cloud infrastructure.
* **The Local Network Mandate:** Existing units operating in the U.S. must be disconnected from public WAN routing. Any communication with Chinese cloud servers for telemetry, model training, or diagnostic logs is legally prohibited.

### The Innovation Dilemma: The Hardware Gap
The ban exposes a massive economic and academic rift. American universities, research labs, and startups are heavily dependent on Chinese quadrupeds due to a massive price-to-performance gap:

| Platform | Manufacturer | Country of Origin | Estimated Base Cost (USD) | Primary Market |
| :--- | :--- | :--- | :--- | :--- |
| **Unitree Go2 Pro** | Unitree Robotics | China | $1,600 | Academic & Developer |
| **Unitree B2** | Unitree Robotics | China | $15,000 | Industrial Research |
| **Spot** | Boston Dynamics | USA | $75,000 | Commercial & Industrial |
| **Vision 60** | Ghost Robotics | USA | $150,000+ | Military & Security |

Robotics researchers have expressed concern regarding the impact of these restrictions. Chris Paxton, a prominent robotics researcher, highlighted the academic cost barrier:
> *"Banning affordable research platforms like Unitree doesn't protect U.S. tech; it forces academic labs to choose between buying one Spot robot for $75,000 or shutting down their quadruped research entirely. We are starving our own student pipeline."*

Eric Jang, VP of AI at Physical Intelligence, has also noted the critical role of cheap hardware in physical AI:
> *"The speed of AI research is directly proportional to the number of physical robots we can run in parallel. If Western labs cannot access high-volume, low-cost hardware, we cede the physical AI learning curve to those who can."*

Conversely, proponents of the ban, including domestic players like Agility Robotics, argue that relying on subsidized, potentially compromised foreign hardware is a structural vulnerability. They point to the historical precedent of DJI in the drone market, arguing that short-term savings in academic research will lead to complete domestic market capitulation.

### The Escape Hatch: "Conditional Approval" Criteria
For defense contractors, federal labs, and select academic institutions, national security agencies (led by the Pentagon's Department of Defense/War) have established a pathway for "Conditional Approval" to operate existing Chinese hardware. To qualify, organizations must implement strict hardening protocols:
1. **Physical RF De-soldering:** Operators must physically disable onboard Wi-Fi and Bluetooth modules. This requires opening the chassis and de-soldering or snipping the coaxial RF antenna connections, forcing the robot to communicate solely via tethered Ethernet or secure, encrypted local micro-radios.
2. **Firmware Sanitization:** The proprietary Unitree operating system and control software must be completely wiped. The robot must be reflashed with an audited, open-source alternative (such as clean ROS2 running on a secured Linux distribution like Ubuntu LTS with real-time RT-PREEMPT patches).
3. **Zero-Trust Intranet Topology:** The robot must operate within a strictly isolated VLAN with no WAN routing. DDS traffic must be isolated using DDS Security extensions (SNDS) or VPN tunnels to prevent local packet injection.

### Reshoring the Western Supply Chain
The FCC ban creates a massive market vacuum. To fill it, Western suppliers must reshore and scale the production of physical AI hardware. However, building an independent supply chain requires overcoming significant manufacturing bottlenecks:
* **Actuator and Motor Density:** Chinese manufacturers benefit from highly integrated local ecosystems for high-torque brushless motors and planetary gear systems. Reshoring requires scaling high-density, low-cost brushless actuators.
* **Strain Wave Gears (Harmonic Drives):** Humanoid and quadruped joint articulation relies heavily on strain wave gears. While companies like Harmonic Drive LLC produce premium gears, they are prohibitively expensive compared to mass-produced Chinese equivalents.
* **Sensing Infrastructure:** Depth cameras, Solid-State LiDARs, and IMUs must be sourced from compliant, non-adversarial manufacturers, bypassing dominant Chinese suppliers like RoboSense or Hesai.

Following the confidential settlement of their long-standing patent dispute in January 2025, Boston Dynamics and Ghost Robotics have advocated for a coordinated U.S. National Robotics Strategy. By pooling resources and calling for federal R&D subsidies, domestic suppliers aim to lower manufacturing costs. 

The long-term outlook depends on whether Western venture capital and federal policy can scale domestic developers like Agility Robotics (Digit), Figure (Figure 02), and Tesla (Optimuses) to a point where secure, Western-made quadrupeds and humanoids can compete on price, not just security compliance. Until then, American robotics research faces a challenging transitional period where security comes at the direct cost of research velocity.

---

# 4. Highlight

## 4.1 Key Questions
1. How will U.S. universities sustain robotics research when forced to transition from $1,600 Chinese platforms to $75,000 domestic alternatives?
2. What are the specific firmware exploits (like BLE command injection and unauthenticated DDS overrides) that prompted the FCC's national security ban?
3. How will Western developers establish competitive, secure supply chains for high-density actuators and harmonic drives to lower domestic hardware costs?

## 4.2 Highlight Text
The FCC’s addition of Chinese quadrupeds and humanoids to its Covered List marks a major shift in the physical AI race. Driven by the GUARD Act (H.R. 9129), this ban addresses critical hardware vulnerabilities—ranging from BLE root command execution to unauthenticated DDS motor-gain hijacking. But security comes at a steep price: academic labs are cut off from affordable $1,600 platforms like Unitree's, while Western equivalents remain 40x more expensive. To maintain its edge in robotics AI, the U.S. must rapidly fund domestic developers and reshore critical component manufacturing.

## 4.3 Hashtags
#Robotics #PhysicalAI #GUARDAct #Cybersecurity #SupplyChain #FCC
