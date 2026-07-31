# **Inside the AV Kill Switch: The Technical and Political Warfare Behind Rep. Kevin Mullin’s Emergency Response Act**

##

On July 28, 2026, outside San Francisco’s historic Fire Station 4, Representative Kevin Mullin (D-CA) stood alongside Mayor Daniel Lurie and public safety officials to announce the introduction of the *Autonomous Vehicle Emergency Response Coordination Act*. The bill represents the first aggressive federal push to establish standardized safety rules governing how driverless vehicle fleets interact with public safety personnel and first responders.

For San Francisco, the legislative move is the culmination of years of escalating friction. Robotaxis have repeatedly blocked fire trucks, run over active fire hoses, and obstructed active crime scenes. In December 2025, during a massive citywide PG&E substation fire that knocked out power to 30% of the city, approximately 1,500 Waymo robotaxis stalled in intersections. Programmed to treat dark traffic signals as four-way stops, the driverless fleet quickly saturated Waymo's remote-assistance queues, paralyzing first responders and delaying an ambulance for 40 minutes. 

Later that month, a stabbing incident on 15th Street in the Mission District saw a Waymo vehicle stop perpendicular to the street, completely blocking a rescue vehicle. Responders knocked on the window to prompt a remote call, but the remote technician could not reposition the car. Firefighters were ultimately forced to enter the driver's seat to move it manually. SFFD logs noted that Waymo's verbal instructions were ineffective, and the vehicle's gear selector malfunctioned, moving forward even when placed in reverse.

### The Technical Battleground: V2X, API Geofencing, and the "Kill Switch"
Rep. Mullin's bill focuses on three primary technical mandates for autonomous vehicle operators:

1. **Dynamic API-Driven Geofencing:** Local public safety dispatchers must be able to issue real-time "geofence notices" to AV fleets. The technical hurdle here is latency and trust. Today, AVs pull dynamic map updates from proprietary cloud-based APIs. Under the new act, these systems must transition to a push architecture where a local municipality can broadcast active emergency perimeters. Security engineers are already raising alarms: how do we prevent GPS spoofing or dynamic geofence injection attacks where a malicious actor mimics emergency dispatch to lock down a city’s transit network?
2. **Standardized V2X Protocols:** While companies like Waymo and Tesla rely heavily on onboard vision and LiDAR, the bill leans toward Vehicle-to-Everything (V2X) communication. The technology has long been stalled in a standards war between DSRC (Dedicated Short-Range Communications, based on IEEE 802.11p) and C-V2X (Cellular V2X, utilizing 3GPP PC5 direct interface). The bill seeks to mandate a unified standard so emergency vehicles can broadcast SRM (Signal Request Messages) and prioritize their paths directly to the AV’s onboard path-planning planner.
3. **Physical Override and the "Remote Kill Switch":** Municipalities are demanding physical override control over driverless cars. If an AV stalls, first responders want a standardized mechanical mechanism (a physical override button or universal key) to put the vehicle in a neutral "freewheel" state. 

### The Political and Economic Standoff
The debate has split Silicon Valley. On one side, AV operators argue that state-by-state or town-by-town local regulations will kill autonomous innovation. On the other, local authorities are demanding physical sovereignty over public roads. 

Garry Tan, President of Y Combinator, expressed frustration on X.com: 
> *"Giving every local municipality veto power or physical override controls over AVs is a regulatory blockade disguised as public safety. We are letting NIMBYism strangle the most important safety technology of the 21st century. Yes, we need APIs for emergency vehicles, but physical override keys will just be abused by local authorities who want to ban autonomous fleets entirely."*

Conversely, former SFFD Fire Chief Jeanine Nicholson has made the municipal position clear: 
> *"We cannot have our firefighters acting as guinea pigs. When a machine blocks a fire truck, lives are lost. If their remote assistance system fails, we need a physical override. Period."*

Waymo's co-CEO, Dmitri Dolgov, took a more technical stance: 
> *"Routing through chaotic edge cases like power outages is the ultimate test of multi-agent path planning. We are actively scaling our remote assistance architecture to prevent queue saturation. However, local physical overrides introduce severe cybersecurity vectors. If a physical bypass can put a 4,000-pound vehicle into neutral, it becomes a target for physical and cyber hijacking."*

Tesla CEO Elon Musk also weighed in, highlighting his aversion to legacy V2X: 
> *"V2X is a crutch. An AV must see and react to emergency lights end-to-end using pure vision neural nets. Relying on government-run road infrastructure is a recipe for failure. That said, standardized physical controls for emergency responders to unlock doors or push a vehicle out of the way make sense, which is why we publish clear First Responder Guides for our fleet."*

With the AV Emergency Response Coordination Act now heading to committee, the industry faces an existential pivot: will autonomous driving remain a purely corporate, proprietary stack, or will it be forced to open its API and mechanical gates to the municipal authorities who run the streets?

---

# 4. Highlight

## 4.1 Key Questions
1. How will AV fleets securely implement dynamic push-based geofencing APIs without exposing themselves to malicious GPS spoofing or network injection attacks?
2. Can C-V2X (direct PC5 interface) overcome the standards inertia of DSRC to become the federally mandated standard for emergency vehicle preemption?
3. How do AV manufacturers design mechanical physical override controls for first responders that do not simultaneously create catastrophic physical hijack vulnerabilities?

## 4.2 Highlight Text
The introduction of the Autonomous Vehicle Emergency Response Coordination Act by Rep. Kevin Mullin (D-CA) marks a federal tipping point for the AV industry. Sparked by critical incidents in San Francisco—like Waymo’s 1,500-vehicle stall during the December 2025 blackout—the bill mandates 24/7 dispatch hotlines, push-API geofencing, and standardized emergency response plans. While local municipalities demand physical override capabilities to clear blocked roads, AV firms warn of cyber-physical hijack risks. Silicon Valley is split: is this a necessary safety framework, or a regulatory blockade of autonomous innovation?

## 4.3 Hashtags
#AutonomousVehicles #V2X #TechRegulation #SelfDrivingCars #PublicSafety #Silicon Valley
