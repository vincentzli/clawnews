# **Apple’s Great Realignment: Inside the 200-Engineer Layoffs, the Siri LLM Overhaul, and the Rise of the Agentic OS under John Ternus**

###

The silicon and software corridors of Cupertino are undergoing their most significant structural shakeup in over a decade. In a series of quiet but sweeping moves, Apple has laid off more than 200 engineers across its Apple Vision Pro and Siri divisions. The timing of this restructuring is highly strategic: it comes just days before John Ternus, Apple’s Senior Vice President of Hardware Engineering, officially succeeds Tim Cook as CEO on September 1, 2026, with Cook transitioning to Executive Chairman of the Board. 

To the casual observer, laying off 200 engineers looks like a reactive cost-cutting exercise in response to cooling hardware sales. However, a deeper look into Apple’s developer tooling, silicon strategy, and architectural pipeline reveals a proactive, multi-year plan. Apple is systematically dismantling its legacy, rule-based voice assistant infrastructure and hardware-first spatial computing hype to fund a massive pivot toward autonomous AI agents. The battle for platform dominance has shifted from the face to the interface, and Apple intends to own the Agentic OS.

#### The Bursting of the Spatial Computing Bubble
For the past two years, the spatial computing narrative has hit a wall of hardware physics and market friction. Apple's Vision Pro, which debuted in 2024 to early adopter hype (shipping between 390,000 and 500,000 units), has seen its consumer momentum evaporate. By the critical fourth quarter of 2025, global shipments collapsed to an estimated 45,000 units. A staggering Bill of Materials (BOM) exceeding $1,500 forced Apple’s hand. Instead of dropping prices to spur consumer demand, Apple took an enterprise-focused turn in June 2026, actually raising the base price from $3,499 to $3,699. 

This pricing adjustment was accompanied by a brutal pruning of internal teams. Apple has largely shut down its in-house Vision Pro gaming division and scaled back the group producing custom Immersive Video content, shifting instead to subsidizing third-party creators. Mark Zuckerberg’s infamous 2024 review of the headset has proven prescient: Zuckerberg argued that Meta's Quest 3 was *"the better product, period,"* pointing out its weight, battery untethering, and superior value. While he later admitted the Vision Pro was excellent for watching movies, the consumer mass-market has rejected $3,500+ face-computers.

Apple is not abandoning spatial computing entirely; visionOS remains a core ecosystem, and a deferred hardware successor is slated for late 2028. However, R&D dollars are being reallocated. Under Ternus, the immediate hardware roadmap is pivoting toward lightweight, AI-powered smart glasses that lack the bulky optics of the Vision Pro but are optimized for contextual, everyday interactions.

#### Tearing Down the Legacy: Rebuilding Siri as an LLM Orchestrator
The engineering headcount saved from the Vision Pro and legacy Siri teams is being redirected into Apple’s most crucial software effort: a complete, ground-up rewrite of its digital assistant. The legacy Siri architecture—a fragile web of semantic parsers, rigid intent matching, and pre-programmed templates (SiriKit)—was structurally incapable of maintaining conversational context. 

According to internal sources, Apple attempted to patch the old codebase with generative AI extensions throughout 2024 and 2025, but the result was sluggish and error-prone, prompting leadership to "tear it to the ground" and deploy a native LLM-based "Siri AI" architecture. Unveiled at WWDC 2026, Siri AI represents a hybrid, secure execution paradigm. 

On-device tasks are handled by Apple Foundation Models (AFMs) with approximately 3 billion parameters. To run these models locally on devices like the iPhone 15 Pro and 16/17 series without consuming excessive RAM, Apple uses aggressive 2-bit quantization, Grouped-Query Attention (GQA), and KV-cache sharing. When queries require complex, multi-step reasoning, the OS routes the semantic graph to Apple's Private Cloud Compute (PCC). PCC runs larger Parallel-Track Mixture-of-Experts (PT-MoE) models on custom Apple Silicon servers, using end-to-end cryptographic isolation to guarantee user privacy.

Crucially, Siri AI is no longer a simple chatbot; it is an autonomous system orchestrator. Using the App Intents framework, Siri AI parses the user’s onscreen awareness and personal context (derived from emails, messages, and photos) to coordinate complex workflows across third-party applications without requiring API wrappers for every individual action.

#### Xcode 27: The Developer’s Agentic Partner
This transition to agentic workflows is also transforming Apple's developer ecosystem. Building on the Model Context Protocol (MCP) support introduced in Xcode 26.3, Xcode 27 shifts the IDE from a code-generation assistant to an autonomous developer partner. 

Through `xcrun mcpbridge`, Xcode 27 exposes an MCP server that allows external AI agents (such as Claude Code or Gemini CLI) to connect directly to the active workspace. Once authorized under Xcode's granular permissions tab in settings, these agents can:
1. Parse the entire project file hierarchy.
2. Build the project and read raw compiler diagnostic logs.
3. Interpret compile-time errors and rewrite code blocks to fix them.
4. Capture SwiftUI Previews as images to verify UI modifications.
5. Run unit and integration tests, iterating autonomously until they pass.

While developers on X and Reddit have praised the capability, they have also highlighted significant friction points. The frequent *"Allow agent to access Xcode?"* permission prompts remain a major UX barrier. More importantly, senior developers warn against letting agents touch the fragile, XML-based `.pbxproj` configuration files, as automated edits frequently result in catastrophic merge conflicts. The community consensus is to let agents write Swift code within files but to handle target creation and file additions manually via the Xcode GUI.

#### The Ternus Era: Reactive Cost-Cutting or Proactive Strategy?
As Tim Cook hands the reins to John Ternus on September 1, 2026, Apple stands at a crossroad. Wall Street bears argue that the layoffs are a reactive surrender, proving that Apple misjudged the spatial computing market and is scrambling to catch up in AI. 

However, tech VCs and analysts see a proactive, multi-year plan. Gene Munster of Deepwater Asset Management argues that the transition will *"supercharge"* Apple’s narrative. Similar to how Cook transitioned the company’s story from hardware sales to recurring "Services" revenue, Ternus has the opportunity to reposition Apple as the definitive leader in consumer AI. Ming-Chi Kuo points to Ternus's technical execution history—specifically leading the Mac transition from Intel to Apple Silicon—as the foundational work that made Apple's on-device AI strategy viable. 

Apple’s vertical integration gives it an advantage. While competitors like Google, Microsoft, and OpenAI are building agents that sit on top of web APIs or browser wrappers, Apple is integrating its agent directly into the hardware and operating system. If Apple can successfully scale Siri AI and Xcode 27 agentic tools, they will capture the agentic AI market before competitors can lock in platform dominance. By sacrificing early-stage hardware experiments like Vision Pro gaming, John Ternus is clearing the runway for Apple's most important product transition since the iPhone: the rise of the Agentic OS.

***
