# Untitled

1. Draft

1.1 Headline
**Who Accesses the Web? The Ninth Circuit's Perplexity Ruling Rewrites the Legal Code for AI Agents**

1.2 Body
On August 4, 2026, the United States Court of Appeals for the Ninth Circuit handed down a historic ruling in *Amazon.com Services, LLC v. Perplexity AI, Inc.* (No. 26-1445). The decision, authored by Circuit Judge Milan D. Smith Jr., vacated a preliminary injunction that had previously blocked Perplexity’s AI-powered agent, "Comet," from accessing Amazon's password-protected servers. In doing so, the court established a massive legal precedent for the future of the agentic web: an AI assistant acting under the explicit direction of a human user is legally a "tool" of the user. Consequently, the user is the one who "accesses" the website—not the AI developer. 

The decision is being cheered by open-web advocates and AI startups, but it has sent shockwaves through the e-commerce and web-publishing sectors. Platforms are realizing that the legal tools they once relied on to block crawlers—specifically the Computer Fraud and Abuse Act (CFAA) and California’s CDAFA—are structurally inadequate against user-delegated AI agents.

### The Technical Anatomy of Perplexity "Comet"

To understand why the court ruled this way, we have to look under the hood of Perplexity's agentic browser architecture. Comet is not a simple backend web scraper. Rather, it is a hybrid Chromium-based agentic browser that combines client-side execution with cloud-based orchestration. 

1. **Chromium Engine Foundation**: Comet is built on a modified Chromium engine. This allows it to run standard browser extensions and interact with web pages exactly like a human user would, rendering JavaScript and executing scripts in real time.
2. **DOM Interpretation Layer**: Rather than performing simple regex searches on raw HTML or scraping pixels, Comet converts the live Document Object Model (DOM) of the active page into a semantic structure of typed objects (e.g., matching a visual button to an interactive `Buy Now` object). This allows the agent to navigate complex, reactive single-page applications (SPAs) with high reliability.
3. **User-Session Context & Cookies**: When a user commands Comet (e.g., "Find the best price for a mechanical keyboard on my Amazon account and add it to my cart"), the agent utilizes the user's active session state and cookies. Because the execution runs locally within the user's browser context, the requests contain valid authentication tokens.
4. **Cloud-Based Multi-Model Orchestration**: While the browser runs locally, the orchestration layer (accessible via the `perplexity.ai` sidecar) sends instructions to Perplexity’s cloud models. These models decompose the user's high-level goal into step-by-step UI actions (clicks, keypresses, navigation), which are then piped back to the local browser extension to execute.

Because Comet uses the user’s actual credentials and browser context to navigate, Amazon's traditional Web Application Firewalls (WAFs) and IP blocklists struggled to isolate the bot. If Amazon blocked the IP addresses routing the traffic, they risked blocking legitimate human buyers. 

### The Legal Conflict: CFAA vs. User Delegation

Amazon sued Perplexity in November 2025, claiming that Comet was engaging in unauthorized access under the CFAA (18 U.S.C. § 1030) and California’s Comprehensive Computer Data Access and Fraud Act (CDAFA). Amazon argued that because they had explicitly issued cease-and-desist letters and updated their `robots.txt` to block Perplexity's bots, any continued automated navigation behind their password barrier constituted federal computer hacking.

In March 2026, Senior U.S. District Judge Maxine Chesney granted Amazon a preliminary injunction, agreeing that Perplexity's workaround constituted "unauthorized access." Perplexity appealed, and the Ninth Circuit panel reversed the decision. 

Writing for the panel, Circuit Judge Milan D. Smith Jr. employed what is now being called the **"Browser Analogy"**:

> "An AI assistant is a tool, not a person for statutory purposes. Just as Apple does not 'access' a website when a user browses the web using Safari, Perplexity does not 'access' Amazon’s servers when a user employs Comet to navigate the web. To hold otherwise would stretch the CFAA beyond its statutory bounds and potentially subject ordinary consumers to criminal liability for using modern browser tools."

The court heavily credited the Electronic Frontier Foundation (EFF), which filed an amicus brief in support of Perplexity, for "articulating the nature of the system most clearly." The EFF warned that expanding the CFAA to cover user-directed browser tools would chill academic research, investigative journalism, and browser customization.

### The Debate: Matthew Prince vs. Aravind Srinivas

The ruling reignites a fierce debate over the "social contract" of the web. Prior to the lawsuit, Cloudflare CEO Matthew Prince published a scathing report accusing Perplexity of "stealth crawling." Prince alleged that Perplexity was bypassing `robots.txt` and rotating IP addresses to spoof Chrome on macOS. Prince didn't mince words, likening the behavior of scraping-focused AI companies to "North Korean hackers" and calling for platforms to "name, shame, and hard block them." He argued that AI "answer engines" destroy the "fair value exchange" of the web:

> "The deal was simple: you let us crawl your site, and we send you traffic. AI engines consume your content but send zero traffic back. It’s an unsustainable extraction."

Perplexity CEO Aravind Srinivas fired back, calling Amazon's legal actions "bullying" and a classic anti-competitive play by incumbents. Srinivas defended the technology using a physical tool analogy:

> "An AI agent is a wrench. If a user owns a wrench and uses it to tighten a bolt on a platform, you don’t sue the wrench manufacturer for trespassing. The user is in control. Platforms cannot dictate what software tools a user is allowed to use to look at public or user-authorized data."

Ben Thompson of *Stratechery* noted that this tension represents a fundamental shift in Aggregator economics. Under Aggregation Theory, platforms like Amazon controlled distribution by owning the consumer relationship. However, if user-delegated AI agents act as the primary interface, they bypass Amazon's ad-supported user experience—threatening Amazon's highly profitable $50 billion retail media business.

### The Technical Retaliation: What Happens Next?

Since platforms can no longer rely on the legal stick of the CFAA to stop agentic browsers, the conflict will shift entirely to technical countermeasures and contract law. Engineers are already proposing new defensive paradigms:

*   **Dynamic DOM Obfuscation**: Generating randomized DOM classes and IDs on every page load to break the semantic mappings used by AI agents.
*   **Behavioral CAPTCHAs**: Analyzing micro-interactions (mouse hover patterns, click acceleration, keypress intervals) to separate human inputs from programmatic DOM injections.
*   **API Rate-Limiting**: Strictly limiting the number of actions a logged-in session can perform per minute, regardless of whether the requests look human.

While the Ninth Circuit's decision is a monumental victory for AI developers, the litigation is far from over. The case has been remanded back to Judge Maxine Chesney to evaluate Amazon's remaining breach-of-contract and terms-of-service claims. In the meantime, the ruling provides a green light for the first generation of fully autonomous AI shoppers.
