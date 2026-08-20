# Inside the DGFiP Cyberattack: The Breach of 678,000 Accounts and the Sovereign AI Controversy

The listing appeared on PwnForums on August 12, 2026, under the handle 'ZeroBytes.' For sale was a database containing the personal and financial records of approximately 678,438 French individuals and businesses. The price tag was set in the thousands of euros, raising critical concerns over the security of public sector IT infrastructure. The exfiltrated data was a dossier of French civic life: reference taxable incomes (RFR), family quotients, source-deducted withholding tax rates, company SIREN numbers, and detailed property surface areas. 

As the details of the breach trickled out, they exposed a widening gap between the French government’s digital ambitions and the security challenges within its legacy administrative networks. It has triggered emergency crisis meetings at the highest levels, a criminal investigation by the Paris prosecutor, and a controversial plan to deploy sovereign artificial intelligence to audit the state’s legacy systems.

### The Silent Vulnerability

At the heart of the breach is the Serveur Professionnel de Données Cadastrales (SPDC), the professional gateway to France's land registry. Governed by the Direction générale des Finances publiques (DGFiP), the SPDC is accessed through the domain `apexappliext.dgfip.finances.gouv.fr`. It is a portal used daily by notaries, land surveyors, and local government officials.

According to cybersecurity audits and subsequent admissions by the ministry, ZeroBytes did not use a sophisticated zero-day exploit to breach this gateway. Instead, they used compromised credentials belonging to a DGFiP employee and an authorized third-party partner. Armed with these credentials, the attacker bypassed the portal's multi-factor authentication (MFA) protocols. 

The security failure is compounded by a damning administrative timeline. The DGFiP’s internal security monitors actually detected the unauthorized access in late June 2026. The agency moved to terminate the fraudulent session and believed the intrusion had been successfully contained. However, for nearly two months, the administration remained entirely unaware that the intruder had already exfiltrated the records of 678,000 taxpayers. The state only realized the extent of the theft when the database was advertised on PwnForums on August 12.

"It is a classic case of detection lag," says a cybersecurity consultant who advises French public institutions, speaking on the condition of anonymity. "Terminating a session is the easy part. Conducting a thorough forensic analysis to determine what data was pulled across the network requires resources that public administrations, burdened by technological debt, simply do not prioritize."

### The Bercy Response

The public revelation of the breach prompted swift, if scrambled, actions from the state. On August 17, 2026, Sébastien Lecornu, in his capacity as France's Prime Minister, convened an emergency interministerial meeting to coordinate a national response. The Paris Public Prosecutor’s Office opened a formal judicial investigation, delegating the case to the Office anticybercriminalité (OFAC).

The following day, August 18, Minister of Public Action and Accounts David Amiel held a joint press conference at Bercy alongside DGFiP Director General Amélie Verdier. Amiel offered an explicit apology to the French public. "Oui, nous nous excusons, parce que ce qui est arrivé est insupportable pour les Français," Amiel stated, acknowledging the severity of the exposure. During the same briefing, Verdier confirmed a third, albeit much smaller, data leak affecting the portal for vacant estates (successions vacantes), though she insisted its scope was minor compared to the SPDC breach.

To prevent similar failures, the government announced a mandate requiring all public sector IT systems and authorized third-party partners to implement strict double-authentication protocols by December 31, 2026. 

However, the most controversial announcement was Amiel’s plan to audit the state’s massive IT infrastructure using advanced artificial intelligence models. The government announced a partnership with French sovereign AI firms, specifically Mistral AI, to perform offensive auditing and scan public networks for vulnerabilities. When asked if the plan included US provider OpenAI, Amiel was categorical: "This excludes OpenAI."

This decision was framed as a defense of technological sovereignty, aimed at ensuring that sensitive maps of public sector IT vulnerabilities are not exposed to foreign jurisdictions subject to legislations like the US Cloud Act.

### The Backlash on the Forums

On online forums like r/france and r/cybersecurity, the reaction from French IT professionals and citizens has been a mixture of anger and dark humor. The disclosure delay has become a primary target of criticism. 

"They detected it in June, closed the door, and went on summer vacation, thinking everything was fine," wrote one user on r/france. "To only find out about the theft because the hacker posted it on a forum is the height of administrative amateurism."

On r/cybersecurity, the discussion focused on the systemic issues plaguing French public IT. Commenters pointed out the irony of the government proposing high-tech AI audits when the administration struggles with basic security hygiene. 

"They are talking about deploying Mistral AI to audit legacy databases, but they couldn't even enforce a working MFA policy on a third-party partner portal," noted a systems administrator in a widely shared post. "You don't need machine learning to tell you that sharing credentials without robust, non-bypassable hardware MFA is a security disaster."

Many comments highlighted the structural recruitment crisis within the DGFiP and other ministries. The public sector's reliance on external contractors is viewed as a direct result of low civil service salaries. In France, a junior Java developer in the public administration starts at a salary that is often 30% to 40% lower than the private sector market rate. Consequently, public IT projects suffer from a massive "technological debt" (dette technologique), characterized by legacy codebases, high staff turnover, and an over-reliance on external consultants who may not be subject to the same security scrutiny as internal staff.

As the Paris prosecutor's office continues its investigation into ZeroBytes, the DGFiP faces the monumental task of notifying 678,000 individuals and businesses that their financial profiles are now in the wild. For the French government, the breach is a reminder that in the era of cyberwarfare, technological sovereignty cannot be bought with AI partnerships alone; it must be built on the unglamorous foundations of basic security hygiene and a fairly compensated IT workforce.
