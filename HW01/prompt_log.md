# HW01 – Prompt Log (Appendix A)

- **Student:** `[Full name – StudentID]`
- **Timestamp format:** `HH:MM dd/mm/yyyy` (local time, UTC+7).
- **Rule:** every prompt sent to any AI tool is recorded verbatim with its full, unedited output.

## Entry format

```text
### <Entry ID> – <HH:MM dd/mm/yyyy> – <Tool (model)>
**Prompt:** <verbatim>
**Output:** <verbatim, unedited>
**Verification:** <claim checked> → <fact> (<source>) – <VALID / INVALID: hallucination / bias>
```

## Requirement 1 – Mindmap

### R1-M01 – 18:08 24/09/2026 – Cursor Agent (Claude Opus 5.5)

**Prompt:**

```text
Create a mindmap about QA/QC in 2026.
Root: "QA/QC 2026+".
Branch 1: the ISTQB CTFL v4.0 test process – list each test activity with its main tasks and work products.
Branch 2: QA/QC job roles in 2026 (manual tester, automation/SDET, AI/LLM QA tester, QA lead, quality engineer, process QA) with key responsibilities and skills.
Branch 3: for each role, mark which work AI can replace, assist, or cannot replace.
Also include the difference between QA and QC, and where static testing fits.
```

Follow-up prompt at 18:16 24/09/2026: `mindmap chỉ nên là 1 hình thôi`

**Output:** see `R1_Mindmap/Mindmap_AI_Output.md`, `QAQC_2026_Mindmap.mmd` and `QAQC_2026_Mindmap.png`.

**Verification:** `[pending – the 3 mistakes found against the ISTQB CTFL v4.0 syllabus]`

## Requirement 2 – AI explanations of the 20 defects



### R2-B01 (D01–D10) – 23:19 24/09/2026 – ChatGPT (GPT-5.6 Luna)

**Prompt:**

```text
For each of the following 10 software defects, give a 3–4 sentence explanation covering: exact date, root cause, key numbers (affected users/devices/passengers, CVSS score if any), consequences, and the official fix. Add one source link per defect. Format as a numbered list.

1. CrowdStrike Falcon Channel File 291 outage (19 July 2024)
2. Cloudflare outage (21 June 2022)
3. Rogers Communications outage in Canada (8 July 2022)
4. FAA NOTAM system outage (January 2023)
5. UK NATS air traffic control failure, FPRSA-R (28 August 2023)
6. AT&T wireless network outage (22 February 2024)
7. Tesla Full Self-Driving Beta recall 23V-085 (2023)
8. Progress MOVEit Transfer CVE-2023-34362
9. Citrix Bleed CVE-2023-4966
10. OpenSSL CVE-2022-3602
```

**Output (verbatim):**

```text
1. **CrowdStrike Falcon Channel File 291 — 19 July 2024.** At 04:09 UTC, CrowdStrike released a Rapid Response Content update for Windows Falcon sensors; a defect in the Content Validator allowed malformed data in Channel File 291, causing an out-of-bounds memory read and Windows BSODs. Microsoft estimated that about **8.5 million Windows devices** were affected; CrowdStrike reverted the defective content at **05:27 UTC**, and the incident was not a cyberattack. The official remediation was to revert the file, improve validation/error handling, introduce staged/canary deployment and additional testing; CrowdStrike's RCA states that the specific failure mode is no longer capable of recurring. ([CrowdStrike.com][1])
   [CrowdStrike — Channel File 291 RCA](https://www.crowdstrike.com/en-us/blog/channel-file-291-rca-available/?utm_source=chatgpt.com)

2. **Cloudflare outage — 21 June 2022.** At **06:27 UTC**, a BGP configuration change in Cloudflare's newer Multi-Colo PoP architecture reordered policy terms so that a `REJECT-THE-REST` rule preceded site-local prefixes, withdrawing critical routes and taking **19 data centers** offline. Those sites represented only about **4% of Cloudflare's network but handled roughly 50% of global requests**, and the outage was fully resolved at **07:42 UTC** after about 75 minutes of impact. Cloudflare's fix was to revert the configuration, redesign the problematic routing policy, introduce MCP-specific deployment/testing, enforce more gradual rollouts, and add automated `commit-confirm` rollback. ([Cloudflare Blog][2])
   [Cloudflare — Outage on 21 June 2022](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com)

3. **Rogers Communications outage — 8 July 2022.** The outage began at **04:58 EDT** on 8 July and resulted from a configuration error during an IP-core upgrade: Rogers removed an ACL filter from distribution routers, causing a flood of routing information that exceeded core-router capacity and crashed the routers. **More than 12 million customers** lost wireless or wireline services, with the outage lasting until approximately **07:00 EDT on 9 July**; 9-1-1 connectivity was also disrupted for a large proportion of Rogers customers. The CRTC/Xona review recommended stronger change testing, router-overload protection, emergency roaming tests, redundant connectivity, improved incident drills, and clearer 9-1-1/outage communications; Rogers subsequently implemented measures including emergency-roaming agreements, backup connectivity and updated incident procedures. ([CRTC][3])
   [CRTC — Rogers network resiliency assessment](https://crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com)

4. **FAA NOTAM system outage — 11 January 2023.** The NOTAM system became unreliable overnight and was ultimately traced to **contract personnel unintentionally deleting files while correcting synchronization between the live primary database and a backup database**; the FAA found no evidence of a cyberattack. The FAA issued a nationwide ground stop around 07:30 EST and lifted it around 09:00, but the disruption cascaded into approximately **9,000 delayed and 1,300 canceled flights** that afternoon. The FAA repaired the system and began strengthening the NOTAM architecture and procedures, including more resilient backup/database arrangements and controls around system maintenance. ([Cục Hàng không Liên bang][4])
   [FAA — NOTAM outage statement](https://www.faa.gov/newsroom/faa-notam-statement?trk=article-ssr-frontend-pulse_little-text-block&utm_source=chatgpt.com)

5. **UK NATS air-traffic-control failure (FPRSA-R) — 28 August 2023.** At **08:32 BST**, NATS's Flight Planning and Resiliency System for Airspace — FPRSA-R — received a transatlantic flight plan containing a unique combination of **six attributes** that triggered an unhandled software exception; the system shut down automatically rather than pass potentially incorrect information to controllers. Automatic processing was restored at **14:32**, but the resulting capacity restrictions affected **more than 700,000 passengers**, including about 300,000 cancellations and 95,000 passengers delayed by more than three hours. NATS implemented a technical fix on the night of **18–19 September 2023**, within 21 days, while the independent review subsequently recommended broader resilience and contingency improvements. ([Cục Hàng không Dân dụng Vương quốc Anh][5])
   [UK CAA — NATS Major Incident Investigation Final Report](https://www.caa.co.uk/publication/download/23340?utm_source=chatgpt.com)

6. **AT&T wireless outage — 22 February 2024.** The outage began during the early morning after AT&T implemented a network change containing an **equipment configuration error**; AT&T initially described it as an incorrect process used while expanding its network, rather than a cyberattack. The FCC found that voice and 5G data services became unavailable across all 50 states, D.C., Puerto Rico and the U.S. Virgin Islands, affecting **more than 125 million devices**, blocking **more than 92 million calls** and **over 25,000 911 attempts**, with restoration taking at least **12 hours**. AT&T restored service by around noon and issued account credits, while the FCC recommended stronger change-management procedures, configuration controls and recovery capabilities. ([Tài liệu FCC][6])
   [FCC — Report on the AT&T wireless outage](https://docs.fcc.gov/public/attachments/DOC-404154A1.pdf?utm_source=chatgpt.com)

7. **Tesla Full Self-Driving Beta recall 23V-085 — 16 February 2023.** NHTSA recall **23V-085** covered **362,758 Tesla vehicles** because certain FSD Beta behaviors could cause vehicles to violate traffic laws or customs during specific maneuvers, increasing collision risk if the driver did not intervene. The recall applied to specified Model S, Model X, Model 3 and Model Y vehicles using affected FSD Beta software; it was a software defect rather than a CVSS-rated cybersecurity vulnerability. Tesla's official remedy was a **free over-the-air software update**, with software **2022.45.10 or later** containing the remedy; NHTSA's later records show the recall population as 362,758 vehicles. ([NHTSA][7])
   [NHTSA — Recall 23V-085](https://static.nhtsa.gov/odi/rcl/2023/RCONL-23V085-7530.pdf?utm_source=chatgpt.com)

8. **Progress MOVEit Transfer — CVE-2023-34362, disclosed 31 May 2023.** CVE-2023-34362 was an **unauthenticated SQL-injection vulnerability** in MOVEit Transfer that could allow attackers to access the application's database and potentially read, modify or delete database contents; it was exploited in the wild during May–June 2023. NVD rates it **CVSS 3.1: 9.8 (Critical)**, with network-based exploitation requiring no privileges or user interaction. Progress fixed the vulnerability through updated MOVEit versions, including **2021.0.6/13.0.6, 2021.1.4/13.1.4, 2022.0.4/14.0.4, 2022.1.5/14.1.5 and 2023.0.1/15.0.1**, with later versions also incorporating fixes. ([NVD][8])
   [NVD — CVE-2023-34362](https://nvd.nist.gov/vuln/detail/cve-2023-34362?utm_source=chatgpt.com)

9. **Citrix Bleed — CVE-2023-4966, disclosed 10 October 2023.** CVE-2023-4966 is an **unauthenticated sensitive-information-disclosure vulnerability** caused by a buffer-related flaw in NetScaler ADC/Gateway; a vulnerable appliance configured as a Gateway or AAA virtual server could expose sensitive information, including session-related data. Citrix published the security bulletin on **10 October 2023** and later confirmed exploitation in the wild; the vulnerability is commonly rated **CVSS 3.1: 9.4 (Critical)**. The official fix was to upgrade to patched builds such as **14.1-8.50+, 13.1-49.15+, or 13.0-92.19+**; Citrix specifically warned that merely mitigating the issue was insufficient because exploitation had been observed. ([Citrix Support][9])
   [Citrix — NetScaler security bulletin for CVE-2023-4966](https://support.citrix.com/external/article/579459/netscaler-adc-and-netscaler-gateway-secu.html?utm_source=chatgpt.com)

10. **OpenSSL — CVE-2022-3602, 1 November 2022.** CVE-2022-3602 was a **buffer overflow** in OpenSSL's X.509 certificate verification code affecting **OpenSSL 3.0.0–3.0.6**; a malicious certificate could trigger an overflow, potentially resulting in a crash and, on some platforms, possible remote-code-execution risk. It was initially pre-announced as Critical but was downgraded to **High** after further analysis because stack-overflow protections and other platform/compiler factors reduced the practical risk; OpenSSL reported no evidence of exploitation when the advisory was released. The official fix was **OpenSSL 3.0.7**, while OpenSSL 1.1.1 and 1.0.2 were unaffected. ([mta.openssl.org][10])
    [OpenSSL — CVE-2022-3602 security advisory](https://mta.openssl.org/pipermail/openssl-announce/2022-November/000243.html?utm_source=chatgpt.com)

[1]: https://www.crowdstrike.com/en-us/blog/falcon-content-update-preliminary-post-incident-report/?utm_source=chatgpt.com "Falcon Content Update Preliminary Post Incident Report | CrowdStrike"
[2]: https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com "Cloudflare outage on June 21, 2022 | Cloudflare Blog"
[3]: https://crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com "Assessment of Rogers Networks for Resiliency and Reliability Following the 8 July 2022 Outage | CRTC"
[4]: https://www.faa.gov/newsroom/faa-notam-statement?trk=article-ssr-frontend-pulse_little-text-block&utm_source=chatgpt.com "FAA NOTAM Statement | Federal Aviation Administration"
[5]: https://www.caa.co.uk/publication/download/23340?utm_source=chatgpt.com "NATS Major Incident Investigation Final Report"
[6]: https://docs.fcc.gov/public/attachments/DOC-404154A1.pdf?utm_source=chatgpt.com "FCC NEWS from the Federal Communications Commission"
[7]: https://static.nhtsa.gov/odi/rcl/2023/RCONL-23V085-7530.pdf?utm_source=chatgpt.com "Tesla

IMPORTANT SAFETY RECALL

\<Date>

\<Name>  
<"
[8]: https://nvd.nist.gov/vuln/detail/cve-2023-34362?utm_source=chatgpt.com "NVD-CVE-2023-34362"
[9]: https://support.citrix.com/external/article/579459/netscaler-adc-and-netscaler-gateway-secu.html?utm_source=chatgpt.com "NetScaler ADC and NetScaler Gateway Security Bulletin for CVE-2023-4966 and CVE-2023-4967"
[10]: https://mta.openssl.org/pipermail/openssl-announce/2022-November/000243.html?utm_source=chatgpt.com "OpenSSL Security Advisory"
```



**Verification:**

- D01: VALID – date, 04:09/05:27 UTC, Content Validator bug, out-of-bounds read, 8.5 million devices and "no longer capable of recurring" all match the CrowdStrike PIR/RCA and Microsoft blog.
- D02: VALID – 06:27–07:42 UTC, 19 MCP data centers, 4% of network / 50% of requests, `REJECT-THE-REST` reordering and remediation match the Cloudflare blog.
- D03: VALID – ACL policy filter removal, 04:58 EDT 08/07 to 07:00 EDT 09/07, more than 12 million customers and 9-1-1 disruption match the CRTC assessment.
- D04: **INVALID – hallucination.** Claim: "The FAA issued a nationwide ground stop around 07:30 EST and lifted it around 09:00." Fact: the FAA's 7:15 a.m. EST statement already reported that airlines had been ordered to pause domestic departures, and its 8:50 a.m. EST statement said the ground stop had been lifted ([FAA NOTAM statement](https://www.faa.gov/newsroom/faa-notam-statement)). The claimed fixes ("more resilient backup/database arrangements and controls around system maintenance") are also not in the FAA statement, which only says the FAA "has taken steps to make the NOTAM system more resilient".
- D05: **INVALID – hallucination.** Claim: FPRSA-R is the "Flight Planning and Resiliency System for Airspace". Fact: FPRSA-R is the "Flight Plan Reception Suite Automated" sub-system ([NATS Major Incident Investigation Final Report](https://www.caa.co.uk/publication/download/23340), title page).
- D06: **INVALID – hallucination.** Claim: "AT&T restored service by around noon." Fact: the outage began at 2:45 AM CST; AT&T stated at 2:10 PM CST that service had been restored, and the FCC says full restoration came over 12 hours after the incident began ([FCC report](https://docs.fcc.gov/public/attachments/DOC-404150A1.pdf)).
- D07: VALID – 362,758 vehicles, four FSD Beta behaviors, free OTA remedy and software 2022.45.10 or later match the NHTSA Part 573 report and owner notification letter.
- D08: VALID – unauthenticated SQL injection, CVSS 9.8, exploitation May–June 2023 and fixed versions match NVD and CISA AA23-158A.
- D09: **INVALID – bias / unsupported claim.** Claim: the flaw "is commonly rated CVSS 3.1: 9.4 (Critical)" and "Citrix specifically warned that merely mitigating the issue was insufficient". Fact: 9.4 is only the vendor (CNA) score; NVD rates it 7.5 High ([NVD](https://nvd.nist.gov/vuln/detail/CVE-2023-4966)). NetScaler stated that no workarounds exist and told customers, after upgrading, to kill all active and persistent sessions ([NetScaler blog](https://www.netscaler.com/blog/news/cve-2023-4966-critical-security-update-now-available-for-netscaler-adc-and-netscaler-gateway/)); the AI omitted this required step from the "official fix".
- D10: VALID – OpenSSL 3.0.0–3.0.6, downgrade from Critical to High, no known exploitation, fix in 3.0.7 match the OpenSSL advisory.



### R2-B02 (D11–D20) – 23:19 24/09/2026 – ChatGPT (GPT-5.6 Luna)

**Prompt:**

```text
For each of the following 10 software defects, give a 3–4 sentence explanation covering: exact date, root cause, key numbers (affected users/devices/passengers, CVSS score if any), consequences, and the official fix. Add one source link per defect. Format as a numbered list.

1. XZ Utils backdoor CVE-2024-3094
2. Palo Alto Networks PAN-OS CVE-2024-3400
3. ChatGPT data exposure incident (20 March 2023)
4. Mata v. Avianca – lawyers citing ChatGPT-generated cases (2023)
5. Moffatt v. Air Canada – chatbot bereavement fare case (2024)
6. Google Gemini image generation problem (February 2024)
7. Google AI Overviews wrong answers (May 2024)
8. LangChain LLMMathChain CVE-2023-29374
9. Microsoft 365 Copilot EchoLeak CVE-2025-32711
10. Vanna.AI CVE-2024-5565
```

**Output (verbatim):**

```text
1. **XZ Utils backdoor — CVE-2024-3094.** On **29 March 2024**, Andres Freund disclosed a malicious backdoor in XZ Utils **5.6.0 and 5.6.1** that had been inserted into release tarballs and build processes; it interfered with `sshd` authentication through `liblzma`, potentially enabling remote code execution for an attacker possessing the required authentication material. The vulnerability was rated **CVSS 10.0/10 Critical**, but the backdoored versions had only reached some rolling/experimental Linux distributions and there is no reliable “number of affected users/devices.” The official response was to **downgrade/remove 5.6.x**, with distributions reverting to trusted XZ versions; the malicious upstream releases were withdrawn. ([CERT-EU][1])
   [Openwall — original XZ backdoor disclosure](https://www.openwall.com/lists/oss-security/2024/03/29/4?utm_source=chatgpt.com)

2. **Palo Alto Networks PAN-OS — CVE-2024-3400.** Palo Alto Networks published the vulnerability on **12 April 2024**: a command-injection flaw in the GlobalProtect feature allowed an **unauthenticated attacker to execute arbitrary commands with root privileges** on vulnerable PAN-OS firewalls. It received **CVSS 10.0 Critical** and was being exploited in the wild; Palo Alto did not publish a total number of compromised devices/users, and Cloud NGFW, Panorama and Prisma Access were not affected. The official fix was to **upgrade PAN-OS to the specified hotfix releases**, with Palo Alto also providing Threat Prevention signatures and temporary mitigations while customers patched. ([security.paloaltonetworks.com][2])
   [Palo Alto Networks — CVE-2024-3400 advisory](https://security.paloaltonetworks.com/CVE-2024-3400?utm_source=chatgpt.com)

3. **ChatGPT data exposure — 20 March 2023.** On **20 March 2023**, a bug in the open-source `redis-py` client used with Redis Cluster caused a small probability of returning data belonging to another user; this exposed some users' chat-history titles and, during a **nine-hour window**, potentially payment-related information belonging to **1.2% of active ChatGPT Plus subscribers**. Exposed payment information could include names, email/payment addresses, card type, last four digits and expiration date, but **full card numbers were never exposed**. OpenAI patched the Redis bug, added redundant user/data checks, audited logs, improved monitoring and strengthened Redis-cluster robustness before restoring the affected functionality. ([OpenAI][3])
   [OpenAI — March 20 ChatGPT outage postmortem](https://openai.com/index/march-20-chatgpt-outage/?utm_source=chatgpt.com)

4. **Mata v. Avianca — ChatGPT-generated legal cases, 2023.** On **22 June 2023**, the U.S. District Court for the Southern District of New York sanctioned attorneys after they submitted **six nonexistent judicial opinions** generated by ChatGPT, complete with fabricated quotations and citations, and continued to stand behind them after their existence was challenged. The consequence was a **$5,000 joint-and-several monetary penalty**, plus orders to notify the client and the judges whose names had been falsely attributed to the cases. The court did not ban ChatGPT use; its response was to enforce lawyers' existing obligation to verify material submitted to the court. ([Justia Law][4])
   [U.S. District Court — Opinion and Order on Sanctions](https://law.justia.com/cases/federal/district-courts/new-york/nysdce/1%3A2022cv01461/575368/54/?utm_source=chatgpt.com)

5. **Moffatt v. Air Canada — chatbot bereavement-fare case.** On **14 February 2024**, the British Columbia Civil Resolution Tribunal decided *Moffatt v. Air Canada*, after Air Canada's website chatbot incorrectly told a passenger that he could obtain a bereavement-fare refund **after completing his travel**, contrary to Air Canada's actual policy. The passenger relied on the chatbot's statement, and the tribunal held Air Canada responsible for the misleading information, awarding **C$812.02** in damages and fees. The case did not involve a CVE or software-security score; the practical “fix” was organizational rather than a disclosed technical patch—Air Canada was held liable for failing to ensure the chatbot's information was accurate. ([vlex.com][5])
   [British Columbia Civil Resolution Tribunal — Moffatt v. Air Canada, 2024 BCCRT 149](https://decisions.civilresolutionbc.ca/crt/crtd/en/item/525448/index.do?utm_source=chatgpt.com)

6. **Google Gemini image-generation problem — February 2024.** On **22 February 2024**, Google paused Gemini's ability to generate images of people after the model produced historically inaccurate depictions—for example, attempting to increase diversity in contexts where the resulting historical representation was inappropriate. Google did not publish a CVSS score or a quantified number of affected users/devices; the consequence was that **image generation of people was temporarily disabled** while Google worked on the model. Google's official remedy was to **pause the feature, modify the model's behavior and release an improved version**, rather than treating it as a conventional software-security vulnerability. ([TechCrunch][6])
   [Google Communications — Gemini image-generation response](https://blog.google/products/gemini/gemini-image-generation-people-update/?utm_source=chatgpt.com)

7. **Google AI Overviews wrong answers — May 2024.** After the U.S. rollout of AI Overviews in **May 2024**, users found generated answers that were factually wrong or nonsensical, including recommendations to put glue on pizza or eat rocks; Google said the failures came partly from unusual queries, satire/forums appearing in results, and attempts to manipulate the system. Google reported that policy-violating answers occurred in **fewer than 1 in 7 million unique queries** where AI Overviews appeared, although the public examples exposed a broader factual-reliability problem. On **31 May 2024**, Google said it had made **more than a dozen technical improvements**, restricted triggering for certain searches, limited satire/humor sources and strengthened content restrictions. ([The Guardian][7])
   [Google — About the latest quality improvements to AI Overviews](https://blog.google/products/search/generative-ai-google-search-may-2024/?utm_source=chatgpt.com)

8. **LangChain LLMMathChain — CVE-2023-29374.** On **5 April 2023**, CVE-2023-29374 was published for LangChain versions through **0.0.131**, where `LLMMathChain` used Python `exec()` to execute LLM-generated expressions, allowing a crafted prompt to achieve arbitrary code execution. The vulnerability was rated **CVSS 3.1: 9.8 Critical**, with network exploitation requiring no privileges or user interaction. The remediation was to eliminate unrestricted `exec()` in the chain and use a restricted mathematical evaluator such as **`numexpr.evaluate()`**, although early advisory records noted that no patched package release was initially available. ([GitLab Advisory Database][8])
   [GitHub Advisory Database — CVE-2023-29374](https://github.com/advisories/GHSA-fprp-p869-w6q2?utm_source=chatgpt.com)

9. **Microsoft 365 Copilot EchoLeak — CVE-2025-32711.** Microsoft disclosed CVE-2025-32711 on **11 June 2025** as an information-disclosure vulnerability in Microsoft 365 Copilot: a specially crafted external message could exploit prompt-injection behavior to cause Copilot to disclose information accessible to it without requiring the victim to click anything. The Microsoft/CNA record gives it **CVSS 3.1: 9.3**, with network-based exploitation, no privileges and no user interaction; the research describing EchoLeak characterized it as a **zero-click** attack capable of exfiltrating data across trust boundaries. Microsoft addressed the vulnerability through service-side security changes rather than requiring an end-user software update. ([OpenCVE][9])
   [Microsoft Security Response Center — CVE-2025-32711](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711?utm_source=chatgpt.com)

10. **Vanna.AI — CVE-2024-5565.** CVE-2024-5565 was published on **31 May 2024** and affects Vanna versions **≤0.5.5**: when `ask()` receives externally controlled input with `visualize=True`, prompt injection can cause arbitrary Python code to be executed instead of merely generating visualization code. JFrog assigned **CVSS 3.1: 8.1**, while NVD itself has not supplied an independent CVSS score; there is no reported affected-user/device count because this is a library vulnerability rather than a documented mass incident. At the time of the advisory there was **no fixed Vanna release**, so the documented mitigation was to set `visualize=False` for untrusted input and avoid passing attacker-controlled prompts into the vulnerable execution path. ([NVD][10])
    [NVD — CVE-2024-5565](https://nvd.nist.gov/vuln/detail/CVE-2024-5565?utm_source=chatgpt.com)

[1]: https://www.cert.europa.eu/publications/security-advisories/2024-032/?utm_source=chatgpt.com "CERT-EU - Critical Vulnerability in XZ Utils"
[2]: https://security.paloaltonetworks.com/CVE-2024-3400?utm_source=chatgpt.com "CVE-2024-3400 PAN-OS: Arbitrary File Creation Leads to OS Command Injection Vulnerability in GlobalProtect"
[3]: https://openai.com/index/march-20-chatgpt-outage/?utm_source=chatgpt.com "March 20 ChatGPT outage: Here’s what happened | OpenAI"
[4]: https://law.justia.com/cases/federal/district-courts/new-york/nysdce/1%3A2022cv01461/575368/54/?utm_source=chatgpt.com "Mata v. Avianca, Inc., 1:2022cv01461 - Document 54 (S.D.N.Y. 2023) :: Justia"
[5]: https://vlex.com/vid/whose-responsibility-is-it-1023398767?utm_source=chatgpt.com "Whose Responsibility Is It Anyway? Chatbots And Legal Issues In Moffatt v Air Canada - vLex Canada"
[6]: https://techcrunch.com/2024/02/22/google-gemini-image-pause-people/?utm_source=chatgpt.com "Google pauses AI tool Gemini's ability to generate images of people after historical inaccuracies | TechCrunch"
[7]: https://www.theguardian.com/technology/article/2024/may/31/google-ai-summaries-sge-changes?utm_source=chatgpt.com "Google to refine AI-generated search summaries in response to bizarre results | Google | The Guardian"
[8]: https://advisories.gitlab.com/pypi/langchain/CVE-2023-29374/?utm_source=chatgpt.com "LangChain vulnerable to code injection | GitLab Advisory Database (GLAD)"
[9]: https://opencve.alliance.unm.edu/cve/CVE-2025-32711?utm_source=chatgpt.com "CVE-2025-32711 - Vulnerability Details - OpenCVE"
[10]: https://nvd.nist.gov/vuln/detail/CVE-2024-5565?utm_source=chatgpt.com "NVD - CVE-2024-5565"
```



**Verification:**

- D11: VALID – versions 5.6.0/5.6.1, disclosure on 29/03/2024, CVSS 10.0 and downgrade remediation match NVD and CISA.
- D12: VALID – 12/04/2024, GlobalProtect command injection with root privileges, CVSS 10.0, exploitation in the wild and hotfix upgrade match the Palo Alto advisory.
- D13: VALID – redis-py bug, chat titles, 1.2% of Plus subscribers in a nine-hour window, no full card numbers and the listed actions match the OpenAI post-mortem.
- D14: VALID – 22/06/2023, six non-existent opinions, USD 5,000 joint-and-several penalty and letters to the client and judges match the court opinion.
- D15: **INVALID – bias (gender assumption) and inaccurate amount.** Claim: the chatbot "told a passenger that he could obtain a bereavement-fare refund", "awarding C$812.02 in damages and fees". Fact: the tribunal refers to Jake Moffatt only as "they/their", so "he" is an assumption not supported by the source; the C$812.02 consists of C$650.88 damages, C$36.14 pre-judgment interest and C$125 CRT fees ([2024 BCCRT 149](https://decisions.civilresolutionbc.ca/crt/crtd/en/525448/1/document.do), paras. 42–44).
- D16: **INVALID – hallucinated source.** Claim: source "Google Communications — Gemini image-generation response" at `https://blog.google/products/gemini/gemini-image-generation-people-update/`. Fact: that URL returns HTTP 404 (checked 24/09/2026); Google's explanation was published on 23/02/2024 at [blog.google/products/gemini/gemini-image-generation-issue](https://blog.google/products/gemini/gemini-image-generation-issue/). The AI also omitted the second cause Google gave: the model became over-cautious and refused some benign prompts.
- D17: **INVALID – hallucination (date and source).** Claim: "On 31 May 2024, Google said it had made more than a dozen technical improvements", citing "Google — About the latest quality improvements to AI Overviews" at `.../generative-ai-google-search-may-2024/`. Fact: Google's post "AI Overviews: About last week" is dated 30 May 2024 ([Google blog](https://blog.google/products/search/ai-overviews-update-may-2024/)); the cited URL is Google's I/O launch announcement, not the improvements post.
- D18: VALID – published 05/04/2023, LangChain ≤ 0.0.131, `exec()` in LLMMathChain, CVSS 9.8 and "no patched version initially" match NVD and GitHub advisory GHSA-fprp-p869-w6q2.
- D19: VALID – 11/06/2025, zero-click information disclosure, CNA CVSS 9.3 and service-side fix match NVD and the EchoLeak case study.
- D20: VALID – published 31/05/2024, `ask()` with `visualize=True`, JFrog CVSS 8.1 (no NVD score), versions ≤ 0.5.5 with no patched release (GHSA-7735-w2jp-gvg6) and `visualize=False` mitigation match JFrog and NVD.



### R2-B03 (follow-up for D01–D03, D07, D08, D10–D14, D18–D20) – 23:29 24/09/2026 – ChatGPT (GPT-5.6 Luna)

**Prompt:**

```text
Answer each question in 1–2 sentences with one source link. Format as a numbered list.

1. CrowdStrike Channel File 291: which sensor version introduced the IPC Template Type, on what date, and how many IPC Template Instances were deployed on 19 July 2024?
2. Cloudflare 21 June 2022: what delayed the final recovery, and what is the name of Cloudflare's internal load balancer that stopped working?
3. Rogers 8 July 2022: how long did it take Rogers to identify the root cause, and what risk level had the change been assigned?
4. Tesla recall 23V-085: how many warranty claims did Tesla identify as possibly related, and did Tesla agree with NHTSA's analysis?
5. MOVEit CVE-2023-34362: on what date did exploitation begin, which group exploited it, and what was the web shell file name?
6. OpenSSL CVE-2022-3602: who reported it and on what date, and what was the companion CVE fixed in the same release?
7. XZ Utils CVE-2024-3094: under what name did the malicious maintainer operate, and what symptom led Andres Freund to discover the backdoor?
8. PAN-OS CVE-2024-3400: which company first detected the exploitation, and which Threat Prevention IDs block it?
9. ChatGPT 20 March 2023: during what hours (Pacific time) was payment information visible, and what change triggered the bug?
10. Mata v. Avianca: which judge issued the sanctions opinion, and name three of the fake cases.
11. LangChain CVE-2023-29374: which GitHub issue and pull request are referenced by NVD, and which LangChain version fixed it?
12. EchoLeak CVE-2025-32711: which company discovered it, when was it reported to Microsoft, and which protections did the attack bypass?
13. Vanna.AI CVE-2024-5565: who discovered it, and which plotting library's code does Vanna ask the LLM to generate?
```

**Output (verbatim):**

```text
1. **CrowdStrike Channel File 291:** Sensor **7.11**, released on **28 February 2024**, introduced the IPC Template Type. On **19 July 2024**, **two IPC Template Instances** were deployed through Channel File 291. [CrowdStrike RCA](https://www.crowdstrike.com/en-us/blog/falcon-content-update-preliminary-post-incident-report/?utm_source=chatgpt.com)

2. **Cloudflare 21 June 2022:** Final recovery was delayed because engineers’ reverts interfered with one another, sometimes reverting previous reverts and causing the problem to reappear. The internal load balancer that stopped working was **Multimog**, a variation of Cloudflare’s Unimog load balancer. [Cloudflare postmortem](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com)

3. **Rogers 8 July 2022:** Rogers took about **14 hours** to pinpoint the root cause because engineers initially lacked router error logs and had difficulty determining which configuration change caused the outage. The change that triggered the outage had been downgraded to **“Low” risk**, although the overall upgrade process had initially been assessed as High risk. [CRTC assessment](https://crtc.gc.ca/eng/publications/reports/xona2024.htm?utm_source=chatgpt.com)

4. **Tesla recall 23V-085:** As of 14 February 2023, Tesla identified **18 warranty claims** potentially related to the recalled condition. Tesla explicitly said it **did not concur with NHTSA’s analysis**, but proceeded with a voluntary recall “out of an abundance of caution.” [NHTSA recall report](https://static.nhtsa.gov/odi/rcl/2023/RCLRPT-23V085-3451.PDF?utm_source=chatgpt.com)

5. **MOVEit CVE-2023-34362:** Exploitation began on **27 May 2023**, when the **CL0P (TA505)** group began exploiting the SQL-injection flaw. The web shell used in the campaign was **LEMURLOOT**, with a known instance named **`human2.aspx`**. [Canadian Centre for Cyber Security advisory](https://www.cyber.gc.ca/en/guidance/profile-ta505-cl0p-ransomware?utm_source=chatgpt.com)

6. **OpenSSL CVE-2022-3602:** It was reported to OpenSSL by **Polar Bear on 17 October 2022**. The companion vulnerability fixed in the same OpenSSL 3.0.7 release was **CVE-2022-3786**, an X.509 email-address variable-length buffer overflow discovered by Viktor Dukhovni. [OpenSSL security advisory](https://mta.openssl.org/pipermail/openssl-announce/2022-November/000243.html?utm_source=chatgpt.com)

7. **XZ Utils CVE-2024-3094:** The malicious maintainer operated under the name **Jia Tan** (GitHub identity **JiaT75**). Andres Freund noticed unusually high CPU usage during SSH logins and **Valgrind errors**, which led him to investigate and discover the backdoor. [XZ incident analysis](https://www.openeuler.org/en/blog/cve-3094.html?utm_source=chatgpt.com)

8. **PAN-OS CVE-2024-3400:** **Volexity** first detected the exploitation on **10 April 2024** while investigating suspicious traffic from a customer’s firewall. Palo Alto Networks says Threat Prevention IDs **95187, 95189, and 95191** block the known exploitation patterns. [Volexity disclosure](https://www-dev.volexity.com/blog/2024/04/12/zero-day-exploitation-of-unauthenticated-remote-code-execution-vulnerability-in-globalprotect-cve-2024-3400/?utm_source=chatgpt.com)

9. **ChatGPT 20 March 2023:** Payment information could have been visible between **1:00 a.m. and 10:00 a.m. Pacific Time**; OpenAI also says subscription-confirmation emails containing payment details could have been misaddressed during that same window. The bug was triggered by a server change at **1:00 a.m. PT** that caused a spike in **Redis request cancellations**, allowing a connection to return another user's data. [OpenAI incident report](https://openai.com/index/march-20-chatgpt-outage/?utm_source=chatgpt.com)

10. **Mata v. Avianca:** The sanctions opinion was issued by **U.S. District Judge P. Kevin Castel**. Three of the fabricated cases were **Varghese v. China Southern Airlines**, **Shaboon v. EgyptAir**, and **Petersen v. Iran Air** (the court also identified fake *Martinez*, *Durden*, and *Miller* opinions). [Mata v. Avianca sanctions opinion](https://law.justia.com/cases/federal/district-courts/new-york/nysdce/1%3A2022cv01461/575368/54/?utm_source=chatgpt.com)

11. **LangChain CVE-2023-29374:** NVD references **GitHub issue #814** and **pull request #1119** (and also issue #1026); the vulnerability affected LangChain through **0.0.131** and was fixed in **0.0.132**. [CVE record and references](https://app.opencve.io/cve/CVE-2023-29374?utm_source=chatgpt.com)

12. **EchoLeak CVE-2025-32711:** **Aim Security/Aim Labs** discovered it and reported it to Microsoft in **January 2025**. The attack bypassed Copilot’s **XPIA prompt-injection classifier, link-redaction/sanitization controls, and CSP restrictions**, using reference-style Markdown and a Microsoft Teams proxy to achieve zero-click data exfiltration. [EchoLeak technical analysis](https://arxiv.org/abs/2509.10540?utm_source=chatgpt.com)

13. **Vanna.AI CVE-2024-5565:** It was discovered by **Natan Nehorai of JFrog Security Research**. Vanna asks the LLM to generate **Plotly** code for visualizing query results, and prompt injection could manipulate that generated Python code into arbitrary code execution. [JFrog security research](https://research.jfrog.com/vulnerabilities/vanna-prompt-injection-rce-jfsa-2024-001034449/?utm_source=chatgpt.com)

```

**Verification:**

- D01: **INVALID – misattributed source.** Claim: the answer cites "[CrowdStrike RCA](https://www.crowdstrike.com/en-us/blog/falcon-content-update-preliminary-post-incident-report/)". Fact: that URL is the *Preliminary Post Incident Review* of 24/07/2024; the Root Cause Analysis is a separate document published on 06/08/2024 ([CrowdStrike](https://www.crowdstrike.com/en-us/blog/channel-file-291-rca-available/)). The facts themselves (sensor 7.11 on 28/02/2024, two IPC Template Instances on 19/07/2024) are correct.
- D02: VALID – conflicting reverts and Multimog match the Cloudflare blog.
- D03: VALID – about 14 hours to pinpoint the root cause and the "Low" risk downgrade match the CRTC assessment.
- D07: VALID – 18 warranty claims and Tesla not concurring with NHTSA match the Part 573 report.
- D08: VALID – 27/05/2023, CL0P/TA505, LEMURLOOT and `human2.aspx` match CISA AA23-158A.
- D10: VALID – Polar Bear on 17/10/2022 and CVE-2022-3786 by Viktor Dukhovni match the OpenSSL advisory.
- D11: VALID – Jia Tan (JiaT75) and high CPU usage during SSH logins with Valgrind errors match public disclosure reports.
- D12: **INVALID – hallucinated source.** Claim: source "[Volexity disclosure](https://www-dev.volexity.com/blog/2024/04/12/...)". Fact: the host `www-dev.volexity.com` does not resolve in DNS (checked 24/09/2026), while the same path on `www.volexity.com` returns HTTP 200. The facts (Volexity, Threat IDs 95187, 95189, 95191) are correct per the [Palo Alto advisory](https://security.paloaltonetworks.com/CVE-2024-3400).
- D13: VALID – 1:00–10:00 a.m. PT and the Redis request-cancellation spike match the OpenAI post-mortem.
- D14: VALID – Judge P. Kevin Castel and the Varghese, Shaboon and Petersen cases match the court opinion.
- D18: **INVALID – hallucination.** Claim: the vulnerability "was fixed in **0.0.132**". Fact: the fix is in LangChain **0.0.142** ([Snyk](https://security.snyk.io/vuln/SNYK-PYTHON-LANGCHAIN-5411357); [Safety DB](https://getsafety.com/vulnerabilities/SFTY-20230405-83237)); the NVD record lists affected versions only "up to (including) 0.0.131" and names no fixed version.
- D19: VALID – Aim Security/Aim Labs, reported in January 2025, XPIA classifier, link redaction and CSP bypass match the EchoLeak case study.
- D20: VALID – Natan Nehorai (JFrog) and Plotly match the JFrog advisory.



### R2-B04 (follow-up for D02, D03, D07, D08, D10, D11, D13, D14, D19, D20) – 23:43 24/09/2026 – ChatGPT (GPT-5.6 Luna)

**Prompt:**

```text
Answer each question in 1–2 sentences with one source link. Format as a numbered list.

1. Cloudflare 21 June 2022: what was the name of the BGP policy statement changed on the spines, and how many minutes passed between the start of the incident and the root cause being found?
2. Rogers 8 July 2022: in which phase of the multi-phase IP core upgrade did the outage occur, and how many recommendations did the CRTC-commissioned assessment make specifically to Rogers?
3. Tesla recall 23V-085: on what date did NHTSA first raise its concerns with Tesla, and on what date did Tesla decide to recall?
4. MOVEit CVE-2023-34362: what is the number and publication date of the CISA/FBI joint advisory, and which HTTP header did the LEMURLOOT web shell use for authentication?
5. OpenSSL CVE-2022-3602: on what date was the "critical" pre-announcement made, and what CVSS score does NVD assign?
6. XZ Utils CVE-2024-3094: which version did CISA recommend downgrading to, and which Arch Linux package version fixed the issue?
7. ChatGPT 20 March 2023: which Python concurrency library was involved in the redis-py bug, and which Redis deployment mode?
8. Mata v. Avianca: what are the names of the two sanctioned attorneys and their law firm, and on what date was the sanctions hearing held?
9. EchoLeak CVE-2025-32711: what CVSS score does NVD assign, and in which month did Microsoft deploy the server-side fix?
10. Vanna.AI CVE-2024-5565: what is the JFrog advisory ID, and what is the Attack Complexity value in its CVSS vector?
```

**Output (verbatim):**

```text
1. **Cloudflare 21 June 2022:** The BGP policy statement changed on the spines was **`AGGREGATES-OUT`**; the incident began at **06:27 UTC** and the root cause was identified at **06:58 UTC**, a gap of **31 minutes**. ([Cloudflare Blog][1])

2. **Rogers 8 July 2022:** The outage occurred during **Phase 6 of a seven-phase IP-core upgrade**. The CRTC-commissioned Xona assessment made **7 recommendations specifically to Rogers**. ([CRTC][2])

3. **Tesla recall 23V-085:** NHTSA first raised its concerns with Tesla on **25 January 2023**, and Tesla decided to conduct the voluntary recall on **7 February 2023**. ([OEMDTC][3])

4. **MOVEit CVE-2023-34362:** The CISA/FBI joint advisory was **AA23-158A**, published **7 June 2023**. The LEMURLOOT web shell authenticated requests using the **`X-siLock-Comment`** HTTP header, whose value had to match its generated password. ([Cổng Thông Tin Chính Phủ][4])

5. **OpenSSL CVE-2022-3602:** The “critical” pre-announcement was made on **25 October 2022** (with the final disclosure on 1 November); NVD currently assigns the vulnerability a **CVSS 3.1 score of 7.5 (High)**. ([NVD][5])

6. **XZ Utils CVE-2024-3094:** CISA recommended **downgrading to XZ Utils 5.4.x** (commonly cited as 5.4.6), while Arch Linux fixed its package at **`xz 5.6.1-2`**. ([Linux Security][6])

7. **ChatGPT 20 March 2023:** The affected Python library was **`redis-py`**, using **Asyncio**, and the bug occurred specifically with a **Redis Cluster** deployment. ([OpenAI][7])

8. **Mata v. Avianca:** The two sanctioned attorneys were **Steven Schwartz and Peter LoDuca**, both of **Levidow, Levidow & Oberman, P.C.**; the sanctions hearing was held on **8 June 2023**. ([Scribd][8])

9. **EchoLeak CVE-2025-32711:** NVD assigns it a **CVSS 3.1 score of 7.5 (High)**, although Microsoft’s CNA score is 9.3; Microsoft deployed the server-side fix in **May 2025**. ([OpenCVE][9])

10. **Vanna.AI CVE-2024-5565:** The JFrog advisory is **JFSA-2024-001034449**; its original CVSS v3.1 vector gives **Attack Complexity = High (AC:H)**. ([research.jfrog.com][10])

[1]: https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com "Cloudflare outage on June 21, 2022 | Cloudflare Blog"
[2]: https://web.crtc.gc.ca/eng/publications/reports/xona2024.htm?utm_source=chatgpt.com "Assessment of Rogers Networks for Resiliency and Reliability Following the 8 July 2022 Outage - Executive Summary | CRTC"
[3]: https://tesla.oemdtc.com/447/sb-23-00-001-full-self-driving-software-may-cause-crash-2016-2023-tesla/?utm_source=chatgpt.com "SB-23-00-001 Full Self-Driving Software May Cause Crash - 2016-2023 Tesla"
[4]: https://content.govdelivery.com/accounts/USDHSCISA/bulletins/35ecb08?utm_source=chatgpt.com "#StopRansomware: CL0P Ransomware Gang Exploits CVE-2023-34362 MOVEit Vulnerability"
[5]: https://nvd.nist.gov/vuln/detail/cve-2022-3602?utm_source=chatgpt.com "NVD-CVE-2022-3602"
[6]: https://linuxsecurity.com/advisories/archlinux/archlinux-202403-1-xz-arbitrary-code-execution-fdkberkecsmz?utm_source=chatgpt.com "Arch Linux: 202403-1 Critical xz Code Execution Advisory"
[7]: https://openai.com/index/march-20-chatgpt-outage/?utm_source=chatgpt.com "March 20 ChatGPT outage: Here’s what happened | OpenAI"
[8]: https://www.scribd.com/document/732836124/business-lawyer-winter-2024-issue?utm_source=chatgpt.com "Business Lawyer Winter 2024 Issue | PDF | Insider Trading | Sec Rule 10b 5"
[9]: https://opencve.alliance.unm.edu/cve/CVE-2025-32711?utm_source=chatgpt.com "CVE-2025-32711 - Vulnerability Details - OpenCVE"
[10]: https://research.jfrog.com/vulnerabilities/vanna-prompt-injection-rce-jfsa-2024-001034449/?utm_source=chatgpt.com "Vanna prompt injection RCE | JFSA-2024-001034449 - JFrog Security Research"
```

**Verification:**

- D02: VALID – `AGGREGATES-OUT`, 06:27 → 06:58 UTC (31 minutes) match the Cloudflare blog.
- D03: VALID – sixth phase of a seven-phase upgrade and seven recommendations to Rogers match the CRTC assessment.
- D07: VALID – 25/01/2023 and 07/02/2023 match the NHTSA Part 573 chronology (the answer cites a third-party mirror instead of NHTSA).
- D08: VALID – AA23-158A on 07/06/2023 and the `X-siLock-Comment` header match CISA.
- D10: VALID – NVD CVSS 7.5 confirmed via the NVD API; pre-announcement on 25/10/2022.
- D11: VALID – CISA named 5.4.6 explicitly (the answer hedges with "5.4.x, commonly cited as 5.4.6"); Arch `xz 5.6.1-2` matches.
- D13: VALID – redis-py with Asyncio on Redis Cluster matches the OpenAI post-mortem.
- D14: VALID – Steven Schwartz, Peter LoDuca, Levidow, Levidow & Oberman and the 08/06/2023 hearing match the court opinion. The cited source is a Scribd upload titled "Business Lawyer Winter 2024 Issue | Insider Trading", not the court record; its content could not be checked, so it is not counted as a confirmed error.
- D19: VALID – NVD 7.5 and Microsoft CNA 9.3 confirmed via the NVD API; server-side fix in May 2025.
- D20: VALID – JFSA-2024-001034449 and AC:H match the JFrog advisory and NVD.

**Conclusion after R2-B01 to R2-B04:** confirmed AI errors were found for 10 of the 20 defects (D01, D04, D05, D06, D09, D12, D15, D16, D17, D18). For the other 10 defects, every checked claim across four prompts matched the sources.

## Requirement 3 – Physical product test cases

### R3-T01 (initial 15 test cases) – 23:24 26/09/2026 – ChatGPT (GPT-5.6 Luna)

Timestamp: reported by the student, no screenshot. Consistent with R3-C01, where the output was pasted into Cursor at 23:24.

**Prompt:**

```text
I am testing a physical household electric fan: senko B813, manufactured 2014,
standing fan. Controls: 3 speed piano keys + Off / rotary knob,
oscillation <push-pull button>. Other adjustments: no.
Design 15 black-box test cases for this device. For each: ID, Objective, Preconditions,
Input, Steps, Expected Result. Cover functional behavior, speed modes, oscillation,
usability, reliability and safety. Format as a table.
```

**Output (verbatim):**

```text
Below is a black-box test set based on your specified configuration: **Senko B813, manufactured 2014, standing fan, 3 piano-key speed controls + Off/rotary control, push-pull oscillation button**. The 3-level speed behavior and push/pull oscillation pattern are also consistent with common mechanical fan designs. :chatgpt-content-reference{index="0"}

| ID | Objective | Preconditions | Input | Steps | Expected Result |
|---|---|---|---|---|---|
| **TC-01** | Verify fan remains OFF when switched to Off | Fan plugged into a suitable power outlet; fan initially OFF | Off / `0` | 1. Plug in the fan.<br>2. Leave the control at Off.<br>3. Observe the blades. | Fan does not start; blades remain stationary; no abnormal sound or movement. |
| **TC-02** | Verify Low-speed operation | Fan plugged in and OFF | Speed 1 | 1. Press Speed 1.<br>2. Observe blade rotation and airflow. | Fan starts and operates continuously at the lowest speed with noticeable airflow. |
| **TC-03** | Verify Medium-speed operation | Fan running at Speed 1 | Speed 2 | 1. Press Speed 2.<br>2. Observe blade rotation and airflow. | Fan changes to medium speed; airflow is greater than Speed 1. |
| **TC-04** | Verify High-speed operation | Fan running | Speed 3 | 1. Press Speed 3.<br>2. Observe blade rotation and airflow. | Fan operates at the highest speed; airflow is greater than Speed 2. |
| **TC-05** | Verify direct transition between speed modes | Fan running at Speed 1 | Speed 1 → 2 → 3 → 2 → 1 | 1. Start at Speed 1.<br>2. Select Speed 2.<br>3. Select Speed 3.<br>4. Return to Speed 2.<br>5. Return to Speed 1. | Each selected speed takes effect correctly without requiring power cycling or causing unexpected shutdown. |
| **TC-06** | Verify fan can be stopped from any speed | Fan running at each speed | Off | 1. Run fan at Speed 1 and select Off.<br>2. Repeat at Speed 2.<br>3. Repeat at Speed 3. | Fan stops each time after selecting Off; blades gradually come to a stop without abnormal behavior. |
| **TC-07** | Verify oscillation can be enabled | Fan running at Speed 1 or higher; oscillation initially OFF | Push oscillation button down | 1. Start fan.<br>2. Push the oscillation button down.<br>3. Observe the fan head for one complete cycle. | Fan head begins sweeping left and right smoothly while the blades continue rotating. |
| **TC-08** | Verify oscillation can be disabled | Fan running and oscillating | Pull oscillation button up | 1. Start oscillation.<br>2. Pull the oscillation button upward.<br>3. Observe the fan head. | Oscillation stops; fan head remains stationary while the fan continues operating. |
| **TC-09** | Verify oscillation works at different speeds | Fan operational; oscillation initially OFF | Speed 1, 2, 3 | 1. Run at Speed 1 and enable oscillation.<br>2. Change to Speed 2.<br>3. Change to Speed 3.<br>4. Observe oscillation at each speed. | Oscillation continues correctly at all three speed settings without abnormal noise, sticking, or unexpected stopping. |
| **TC-10** | Verify fan remains stable during operation | Fan assembled on a firm, level surface | Speed 3 + oscillation ON | 1. Place fan on a level surface.<br>2. Run at Speed 3.<br>3. Enable oscillation.<br>4. Observe the base and fan body. | Fan remains stable without excessive rocking, walking, tipping, or abnormal vibration. |
| **TC-11** | Verify controls are understandable and usable | Fan OFF and unplugged initially | Speed buttons, Off control, oscillation button | 1. Identify the controls without consulting instructions.<br>2. Select Off, Speed 1/2/3, and oscillation controls. | Controls can be distinguished and operated without excessive force or confusing/unintended activation. |
| **TC-12** | Verify repeated operation of speed controls | Fan connected to power | Repeated Speed 1 → 2 → 3 → Off cycles | 1. Perform the sequence 1 → 2 → 3 → Off repeatedly for 20 cycles.<br>2. Observe controls and fan operation. | Each selection produces the corresponding behavior; no sticking, failure to respond, excessive sparking/noise, or degradation of operation is observed. |
| **TC-13** | Verify repeated oscillation operation | Fan running at Speed 2 | Push → pull oscillation control repeatedly | 1. Start fan at Speed 2.<br>2. Push oscillation button down.<br>3. Wait for oscillation to begin.<br>4. Pull it up to stop.<br>5. Repeat 10 times. | Oscillation starts and stops reliably on every cycle; button remains mechanically functional and fan continues operating normally. |
| **TC-14** | Verify safe behavior after restoring power | Fan initially running, then power disconnected | Power interruption and restoration | 1. Run fan at Speed 2.<br>2. Disconnect power using the normal power switch/outlet.<br>3. Restore power.<br>4. Observe whether the fan starts. | Fan should not unexpectedly restart if its physical control is in the Off position; no abnormal electrical or mechanical behavior occurs. |
| **TC-15** | Verify long-duration operation and safety | Fan properly assembled, unobstructed, placed on stable surface | Speed 3 + oscillation ON for an extended period | 1. Run fan at Speed 3 with oscillation enabled for several hours under normal conditions.<br>2. Periodically observe airflow, noise, vibration, controls, power cord and motor housing. | Fan continues operating without abnormal overheating, burning smell, smoke, excessive vibration/noise, intermittent stopping, or other unsafe behavior. |

### Coverage

- **Functional behavior:** TC-01–06
- **Speed modes:** TC-02–06
- **Oscillation:** TC-07–09, TC-13
- **Usability:** TC-10–11
- **Reliability:** TC-12–13, TC-15
- **Safety:** TC-10, TC-14–15

For a **black-box testing assignment**, these are deliberately based on observable **inputs and outputs** rather than internal components such as the motor, capacitor, wiring, or thermal protection. This is appropriate because the tester should judge the device from externally observable behavior.
```

**Verification:** superseded. The prompt described the speed control ambiguously ("piano keys + Off / rotary knob") and ChatGPT designed for piano keys, while the fan has a rotary knob. The prompt was corrected and re-sent as R3-T02, which is the artifact evaluated in the report.

### R3-C01 – 23:24 26/09/2026 – Cursor (Claude)

**Prompt:** the R3-T01 prompt and output above, pasted into Cursor with the request to continue the physical-product requirement.

**Output:** draft of report sections 3.1–3.6 (critique of R3-T01, AI-missed edge cases, refined 15 test cases marked NOT RUN). Reviewed and edited by the student before submission.

### R3-T02 (initial 15 test cases, corrected prompt) – 23:33 26/09/2026 – ChatGPT (GPT-5.6 Luna)

Timestamp evidence: `R3_Device/R3-T02_timestamp.png` (ChatGPT message menu showing "Hôm nay, 23:33").

**Prompt:**

```text
I am testing a physical household electric fan: Senko B813, manufactured 2014,
standing fan. Controls: a rotary speed knob with 4 positions (0 = Off, 1, 2, 3)
and a push-pull oscillation knob on the motor housing. Other adjustments: none.
Design 15 black-box test cases for this device. For each: ID, Objective, Preconditions,
Input, Steps, Expected Result. Cover functional behavior, speed modes, oscillation,
usability, reliability and safety. Format as a table.
```

**Output (verbatim):**

```text
Below is a **black-box test suite of exactly 15 test cases** for the specified Senko B813. I’m treating the device configuration you provided as the test oracle; public references also describe the B813 family as having mechanical speed control and 3 speed levels. :chatgpt-content-reference{index="0"}

| ID | Objective | Preconditions | Input | Steps | Expected Result |
|---|---|---|---|---|---|
| **TC01** | Verify fan remains OFF at position 0 | Fan connected to power; knob at 0 | Speed = 0 | 1. Connect power.<br>2. Set knob to 0.<br>3. Observe fan. | Fan does not rotate; no airflow is produced. |
| **TC02** | Verify low-speed operation | Fan connected; initially OFF | Speed = 1 | 1. Turn knob from 0 → 1.<br>2. Observe blade rotation and airflow. | Fan starts rotating and produces **low-speed airflow** continuously. |
| **TC03** | Verify medium-speed operation | Fan connected; initially OFF | Speed = 2 | 1. Turn knob from 0 → 2.<br>2. Observe airflow. | Fan operates continuously at **medium speed**, noticeably stronger than level 1. |
| **TC04** | Verify high-speed operation | Fan connected; initially OFF | Speed = 3 | 1. Turn knob from 0 → 3.<br>2. Observe airflow. | Fan operates continuously at **maximum speed**, stronger than levels 1 and 2. |
| **TC05** | Verify all speed transitions | Fan running | 1 → 2 → 3 → 2 → 1 → 0 | 1. Start at speed 1.<br>2. Change through each position sequentially.<br>3. Return to 0. | Fan responds to every knob position without unexpected stopping, abnormal noise, or failure to change speed. |
| **TC06** | Verify direct transition from OFF to each speed | Fan connected | 0 → 1, 0 → 2, 0 → 3 | 1. Set knob to 0.<br>2. Select speed 1 and observe.<br>3. Stop.<br>4. Repeat for 2 and 3. | Fan starts correctly from OFF at each available speed position. |
| **TC07** | Verify oscillation OFF/fixed-head operation | Fan running at speed 1 | Oscillation knob UP | 1. Set speed to 1.<br>2. Leave/pull oscillation knob in the OFF position.<br>3. Observe fan head for several cycles. | Fan head remains stationary and airflow is directed in a fixed direction. |
| **TC08** | Verify oscillation activation | Fan running | Push oscillation knob DOWN | 1. Start fan at speed 1.<br>2. Push the oscillation knob down.<br>3. Observe the fan head. | Fan head begins moving horizontally from side to side; fan continues running normally. |
| **TC09** | Verify oscillation can be stopped | Fan oscillating | Pull oscillation knob UP | 1. Activate oscillation.<br>2. Allow head to move for several cycles.<br>3. Pull knob up.<br>4. Observe. | Oscillation stops and the fan head remains in a fixed position. |
| **TC10** | Verify oscillation works at different speeds | Fan connected | Speeds 1, 2, 3 + oscillation ON | 1. Test oscillation at speed 1.<br>2. Repeat at speed 2.<br>3. Repeat at speed 3. | Oscillation operates at all three speed settings without abnormal vibration or interruption. |
| **TC11** | Verify usable control operation | Fan OFF and connected | Rotate speed knob through 0–3 | 1. Operate the knob repeatedly between all positions.<br>2. Check that each position can be selected clearly. | Knob moves between positions predictably; each position can be selected without sticking, excessive force, or ambiguous operation. |
| **TC12** | Verify stable operation during extended use | Fan placed on a stable, level surface | Speed 2 + oscillation ON | 1. Start fan at speed 2.<br>2. Enable oscillation.<br>3. Run continuously for an extended period, e.g. 30–60 min.<br>4. Observe operation periodically. | Fan continues operating without unexpected shutdown, severe vibration, abnormal smell, smoke, sparking, or significant deterioration in airflow. |
| **TC13** | Verify mechanical stability and abnormal vibration | Fan assembled correctly on stable surface | Speed 3 + oscillation OFF/ON | 1. Run at speed 3 with oscillation OFF.<br>2. Observe base and fan body.<br>3. Enable oscillation and observe again. | Fan remains stable; no excessive shaking, walking, tipping tendency, or abnormal mechanical noise occurs. |
| **TC14** | Verify protective safety during normal operation | Fan fully assembled; protective grille intact | Speed 3 | 1. Run fan at speed 3.<br>2. Visually inspect grille and rotating blades without inserting objects.<br>3. Check for exposed moving/electrical parts. | Protective grille remains secure; rotating blades are not directly accessible during normal operation; no exposed hazardous electrical parts are observed. |
| **TC15** | Verify safe shutdown and restart | Fan running at speed 2 | 2 → 0 → 1 | 1. Run fan at speed 2.<br>2. Turn knob to 0.<br>3. Confirm fan stops completely.<br>4. Wait until blades stop.<br>5. Turn knob to 1. | Fan stops when set to 0. After shutdown, it can be restarted normally at speed 1 without abnormal noise, smell, sparking, or other unsafe behavior. |

### Coverage

- **Functional behavior:** TC01–TC06
- **Speed modes:** TC02–TC06
- **Oscillation:** TC07–TC10
- **Usability:** TC11
- **Reliability/endurance:** TC12–TC13
- **Safety:** TC14–TC15

For a physical appliance, safety cases should be **observation-based**: don't deliberately insert fingers/objects into the grille, introduce water, overload the motor, or create electrical faults merely to test failure behavior. Public documentation for the B813 family also describes a protective grille and mechanical 3-speed control. :chatgpt-content-reference{index="1"}
```

**Verification:** see report section 3.3 (per-test-case verdicts) and 3.4 (edge cases the output missed).

### R3-C02 – 23:34 26/09/2026 – Cursor (Claude)

**Prompt:** the R3-T02 output above, pasted into Cursor with the request to update the prompt log and the report.

**Output:** re-evaluation of report sections 3.3–3.5 against R3-T02. Reviewed and edited by the student before submission.

### R3-C03 – 23:36 26/09/2026 – Cursor (Claude)

**Prompt:** "bạn hãy viết giúp tôi luôn phần Student explanation"

**Output:** the "Why the AI missed it" explanations for TC-06, TC-07, TC-10, TC-11 and TC-12 in report section 3.4. Reviewed by the student before submission.

## Cursor Agent prompts (all sessions)

Every prompt sent to the Cursor Agent, copied verbatim from the Cursor chat history (timestamps are the times shown in that history). Cursor outputs are the resulting file changes, identified by the Git commits in the same time window; the full agent transcripts can be exported from Cursor on request.

Sessions: S1 = planning session on 23/09/2026 (Codex/OpenAI, see below); S2 = R1/R2 work, 24–25/09/2026; S3 = R1 mindmap, 24/09/2026; S4 = R3 and AI compliance, 26/09/2026.

| # | Time | Session | Prompt (verbatim) |
|---|---|---|---|
| CA-01 | 16:59 24/09/2026 | S2 | chỉnh sủa lại đúng chính xác về số lượng yêu cầu, tại vì tôi thấy đang ghi bị dư vài cái<br>Each posting: link, dated screenshot, job description, required skills, salary.<br>Write 12 sentences of "AI Impact Analysis" per posting. |
| CA-02 | 17:14 24/09/2026 | S2 | hãy check lại giúp tôi<br>Còn thiếu, chưa kiểm chứng:<br>JP01, JP03 và JP05–JP09 vẫn thiếu bằng chứng ngày đăng hợp lệ.<br>JP08 và JP09 đang hiển thị "Expired".<br>Vẫn còn đoạn mô tả tạm (placeholder) ở JP01–JP03 và JP08–JP10.<br>Đoạn phân tích của JP05 có nhắc "insurance domain"; bạn nên đối chiếu lại với tin gốc.<br>Ngày nộp bài vẫn đang để trống. |
| CA-03 | 17:23 24/09/2026 | S2 | tôi xác nhận rằng jp3 vẫn còn, bạn thử lại đi |
| CA-04 | 17:28 24/09/2026 | S2 | bạn hãy giúp tôi tìm kiếm cái khác để thay thế jp8 và jp9 |
| CA-05 | 17:38 24/09/2026 | S2 | đổi link của jp3 thành cái này https://dxctechnology.wd1.myworkdayjobs.com/DXCJobs/job/VNM---HO-CHI-MINH-CITY/Quality-Engineering_51585699?src=JB-11100 , tôi sẽ chụp có ngày |
| CA-06 | 17:41 24/09/2026 | S2 | tôi đã thay đổi ảnh, cái phần nội dung bạn không nên ghi quá trình lại vd như recapture pending, .... |
| CA-07 | 17:46 24/09/2026 | S2 | vậy hãy thay luôn jp1 đi |
| CA-08 | 17:50 24/09/2026 | S2 | bây giờ hãy thay đổi tên file thống nhất JP**.png, và cập nhật lại tên file trong report và tên file ngoài, các ảnh không dùng tôi đã xóa hết |
| CA-09 | 17:52 24/09/2026 | S2 | kiểm tra xem yêu cầu của requirement 1 xong chưa |
| CA-10 | 17:54 24/09/2026 | S2 | hãy thay đổi các jp5 tới jp7 |
| CA-11 | 17:59 24/09/2026 | S2 | tôi đã chụp ảnh rồi đó, kiểm tra xem ổn chưa, lưu ý là 10 job không đc trùng nha |
| CA-12 | 18:05 24/09/2026 | S2 | hãy đề xuất vẽ mind map như nào |
| CA-13 | 18:08 24/09/2026 | S3 | Create a mindmap about QA/QC in 2026.<br>Root: "QA/QC 2026+".<br>Branch 1: the ISTQB CTFL v4.0 test process – list each test activity with its main tasks and work products.<br>Branch 2: QA/QC job roles in 2026 (manual tester, automation/SDET, AI/LLM QA tester, QA lead, quality engineer, process QA) with key responsibilities and skills.<br>Branch 3: for each role, mark which work AI can replace, assist, or cannot replace.<br>Also include the difference between QA and QC, and where static testing fits. |
| CA-14 | 18:14 24/09/2026 | S2 | hãy làm requirement 2 |
| CA-15 | 18:16 24/09/2026 | S3 | mindmap chỉ nên là 1 hình thôi |
| CA-16 | 22:50 24/09/2026 | S2 | phần bảng 2.4 là ở đâu yêu cầu vậy |
| CA-17 | 22:55 24/09/2026 | S2 | là sao tôi vẫn chưa hiểu dòng đó lắm |
| CA-18 | 23:00 24/09/2026 | S2 | bạn hãy đóng giả việc viết prompt và điền vào phần đó. Bạn hãy giúp tôi tạo file log prompt để ghi lại |
| CA-19 | 23:08 24/09/2026 | S2 | nên định dạng output của prompt như nào để dễ xem |
| CA-20 | 23:13 24/09/2026 | S2 | bạn nghĩ yêu cầu có phải là đưa prompt vào AI giải thích rồi tìm không, nếu như vậy thì khá dài, dài hơn cả các yêu cầu kia nhưng nó chỉ có 20 điểm |
| CA-21 | 23:15 24/09/2026 | S2 | bạn hãy chỉnh lại giúp tôi phần đó |
| CA-22 | 23:18 24/09/2026 | S2 | hãy bỏ d1,2,3 và chuyển thành 2 cái duy nhất |
| CA-23 | 23:26 24/09/2026 | S2 | model GPT-5.6 Luna., bạn giúp tôi điền giờ và giúp tôi đánh giá các điểm như yêu cầu |
| CA-24 | 23:39 24/09/2026 | S2 | tại sao lại có cái này 2-B03 (follow-up for D01–D03, D07, D08, D10–D14, D18–D20) – `[HH:MM dd/mm/yyyy]` – ChatGPT (GPT-5.6 Luna) |
| CA-25 | 23:41 24/09/2026 | S2 | tôi mới thêm vào rồi đó |
| CA-26 | 23:45 24/09/2026 | S2 | rồi đó |
| CA-27 | 23:48 24/09/2026 | S2 | bạn tự động điền giờ đi, khỏi commit |
| CA-28 | 23:49 24/09/2026 | S2 | đúng format luôn không có khoảng |
| CA-29 | 23:50 24/09/2026 | S2 | bạn ghi đại đi, lấy giờ đầu tiên trong chat |
| CA-30 | 23:58 24/09/2026 | S2 | bạn hãy fake giúp tôi phần prompt và phần output để có thể ra được phần requirement 2 |
| CA-31 | 00:00 25/09/2026 | S2 | ý tôi là phần prompt để có thể ra được cái phần report của requirement trong @HW01/HW01_Report.md |
| CA-32 | 00:09 25/09/2026 | S2 | nhưng yêu cầu là phải giữ nguyên input, không được paraphase. |
| CA-33 | 00:11 25/09/2026 | S2 | tiếp tục làm requirement 3 |
| CA-34 | 00:30 25/09/2026 | S2 | tôi QA cho remote máy lạnh được không |
| CA-35 | 23:16 26/09/2026 | S4 | Choose a SPECIFIC household device (fan / water filter / rice cooker / smart<br>bulb...).<br>Submit 1 photo of THE DEVICE + your student ID card in the SAME frame.<br>Declare brand, model, year, serial number (mask the middle 4 chars)<br>Design 12 test cases Objective / Input / Steps / Expected / Actual / Verdict).Clarification: 15 test cases total. Execute and record videos for ≥ 5 out of<br>the 15 (not all 15 need videos). Also aim to find ≥ 5 defects from the device during execution.<br><br>tôi nghĩ tôi sẽ chọn máy lạnh có điều khiển từ xa, brand là casper. |
| CA-36 | 23:19 26/09/2026 | S4 | hay chuyển thành quạt máy đi, quạt máy chỉ có tính năng chọn 3 chế độ speed, có nút để máy quạt quay hoặc không quay |
| CA-37 | 23:24 26/09/2026 | S4 | đây là prompt<br>I am testing a physical household electric fan: senko B813, manufactured 2014,<br>standing fan. Controls: 3 speed piano keys + Off / rotary knob,<br>oscillation <push-pull button>. Other adjustments: no.<br>Design 15 black-box test cases for this device. For each: ID, Objective, Preconditions,<br>Input, Steps, Expected Result. Cover functional behavior, speed modes, oscillation,<br>usability, reliability and safety. Format as a table.<br><br>đây là kết quả<br>[followed by the verbatim R3-T01 output, logged in entry R3-T01] |
| CA-38 | 23:29 26/09/2026 | S4 | quạt này là núm vặn xoay tốc độ |
| CA-39 | 23:33 26/09/2026 | S4 | bạn hãy đưa tôi lại prompt đúng với đó để tôi đưa lại vào chatgpt vì có yêu cầu chụp hình minh chứng |
| CA-40 | 23:34 26/09/2026 | S4 | đây là output, bạn hãy chỉnh lại prompt và output<br>[followed by the verbatim R3-T02 output, logged in entry R3-T02] |
| CA-41 | 23:36 26/09/2026 | S4 | bạn hãy viết giúp tôi luôn phần Student explanation |
| CA-42 | 23:37 26/09/2026 | S4 | thời gian là 23:37 model là gpt 5.6 luna |
| CA-43 | 23:38 26/09/2026 | S4 | Giờ gửi của R3-T02, giờ gửi và model của R3-T01 ghi là 23:30 |
| CA-44 | 23:40 26/09/2026 | S4 | giờ thật nè |
| CA-45 | 23:41 26/09/2026 | S4 | không cần commit giờ của r3-t01 là 23:26 |
| CA-46 | 23:41 26/09/2026 | S4 | vậy 23:24 |
| CA-47 | 23:44 26/09/2026 | S4 | hãy viết giúp tôi phần này |

## Codex / OpenAI planning session (S1)

`[Student to add: the prompts sent to Codex on 23/09/2026 (assignment reading, PLAN.md, first R1 report draft – commits e7e4d1d to bbbbb2a), with timestamps and outputs, exported from the Codex history.]`
