# HW01 – Prompt Log (Appendix A)

- **Student:** `[Full name – StudentID]`
- **Timestamp format:** `HH:MM dd/mm/yyyy` (local time, UTC+7)
- **Rule:** every prompt sent to any AI tool is recorded verbatim with its full, unedited output.

## Entry format

```text
### <Entry ID> – <HH:MM dd/mm/yyyy> – <Tool (model)>
**Prompt:** <verbatim>
**Output:** <verbatim, unedited>
**Verification:** <claim checked> → <fact> (<source>) – <VALID / INVALID: hallucination / bias>
```

## Requirement 1 – Mindmap

### R1-M01 – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:**

**Output:** see `R1_Mindmap/Mindmap_AI_Output.md`

## Requirement 2 – AI explanations of the 20 defects



### R2-D01 – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:** Explain the CrowdStrike Falcon outage of July 2024 (Channel File 291): root cause, exact date and time, number of affected devices, severity, consequences and the official fix. Cite your sources.

**Output (verbatim):**

> The **CrowdStrike Falcon outage on July 19, 2024** was caused by a faulty security-content update—specifically **Channel File 291**—that crashed Windows machines. It was **not a cyberattack**. CrowdStrike's later Root Cause Analysis (RCA) gives the clearest technical explanation. ([CrowdStrike.com](http://CrowdStrike.com))
>
> ### 1. Exact date and time
>
> - **Date:** Friday, **July 19, 2024**
> - **Faulty update released:** **04:09 UTC**
> - **Update reverted:** **05:27 UTC**
> - **Exposure window:** **78 minutes**
> - In Vietnam time (UTC+7): **11:09–12:27 on July 19**.
> - Affected systems were Windows hosts running **Falcon Sensor 7.11+** that were online and received the problematic content during that window. Linux and macOS were not affected. ([CrowdStrike.com](http://CrowdStrike.com))
>
> ### 2. What exactly went wrong?
>
> This is the interesting part.
>
> CrowdStrike's Falcon sensor uses **Rapid Response Content**—configuration data that can be delivered without updating the entire Falcon sensor. This content is delivered through **Channel Files**.
>
> Channel File **291** was responsible for detecting malicious activity involving Windows **named pipes**. ([CrowdStrike.com](http://CrowdStrike.com))
>
> The underlying bug was a **parameter-count mismatch**:
>
> ```text
> IPC Template Type
>         ↓
> expected: 21 inputs
>         ↓
> actual sensor code supplied: 20 inputs
>         ↓
> Channel File 291 referenced input #21
>         ↓
> Content Interpreter read beyond the array
>         ↓
> out-of-bounds memory read
>         ↓
> Windows kernel crash / BSOD
> ```
>
> CrowdStrike's RCA says the IPC Template Type defined **21 input fields**, while the integration code supplied only **20**. This mismatch escaped validation and testing.
>
> The July 19 update introduced a Template Instance that actually used the **21st field** rather than treating it as a wildcard. The Content Interpreter therefore attempted to access a 21st value that did not exist, producing an **out-of-bounds memory read** and ultimately a system crash.
>
> So the root cause wasn't simply "a bad file." It was the combination of:
>
> 1. **21 fields expected vs. 20 actually supplied**
> 2. A **missing runtime bounds check**
> 3. Testing that didn't exercise a non-wildcard condition on the 21st field
> 4. A **Content Validator logic error** that allowed the problematic configuration through.
>
> ### 3. How many devices were affected?
>
> Microsoft estimated approximately **8.5 million Windows devices**, representing **less than 1% of all Windows machines**. ([The Official Microsoft Blog](https://blogs.microsoft.com/blog/2024/07/20/helping-our-customers-through-the-crowdstrike-outage/?utm_source=chatgpt.com))
>
> The relatively small percentage is important: CrowdStrike had enormous enterprise penetration, so a failure affecting <1% of Windows machines could still affect a huge number of organizations and critical services.
>
> ### 4. Severity and consequences
>
> Technically, the failure was severe because the affected machines could **crash at the operating-system level and become stuck in a BSOD/reboot cycle**, rather than merely having the security product stop working.
>
> The disruption propagated across sectors including:
>
> - ✈️ **Airlines and airports** — flight operations and check-in systems were disrupted.
> - 🏥 **Healthcare** — hospitals and healthcare providers experienced IT disruptions.
> - 🏦 **Financial services** — banks and other financial organizations were affected.
> - 🚨 **Emergency services** — some emergency-service operations experienced disruption.
> - 🛒 **Retail** — stores and retail systems were affected.
> - 📰 **Media and other businesses** — numerous organizations experienced operational interruptions.
>
> The U.S. Congressional Research Service summarized the incident as causing global disruption across **aviation, emergency services, financial services, healthcare, and retail**, while citing Microsoft's estimate of 8.5 million affected Windows systems. ([Quốc hội Mỹ](https://www.congress.gov/crs_external_products/IN/PDF/IN12392/IN12392.2.pdf?utm_source=chatgpt.com))
>
> One important distinction: **CrowdStrike's own cloud/Falcon platform was not itself down.** The problem was with Falcon sensor content running on customers' Windows endpoints. CrowdStrike explicitly stated that Falcon Complete and OverWatch services were not disrupted. ([CrowdStrike.com](http://CrowdStrike.com))
>
> ### 5. What was the official fix?
>
> There were several layers of remediation.
>
> **Immediate fix — July 19**
>
> CrowdStrike **reverted the problematic Channel File 291 content at 05:27 UTC**. New or unaffected machines therefore did not receive the faulty configuration. ([CrowdStrike.com](http://CrowdStrike.com))
>
> For machines already stuck in the crash loop, administrators had to use recovery procedures, including Safe Mode/Windows Recovery, and remove the problematic:
>
> ```text
> C:\Windows\System32\drivers\CrowdStrike\C-00000291*.sys
> ```
>
> Microsoft subsequently provided an automated recovery tool for affected Windows clients, servers and Hyper-V VMs. ([Hỗ Trợ Microsoft](https://support.microsoft.com/en-us/servicing/os/windows/2024/07/kb5042429-new-recovery-tool-to-help-with-crowdstrike-issue-impacting-windows-devices?utm_source=chatgpt.com))
>
> **Permanent technical fixes**
>
> CrowdStrike subsequently:
>
> - Added **runtime array-bounds checks** to prevent the out-of-bounds read.
> - Corrected the IPC Template Type to provide **21 inputs**.
> - Added compile-time validation of Template Type input counts.
> - Expanded tests to include **non-wildcard matching for every field**.
> - Added additional Content Validator checks.
> - Added **staged/canary deployment** for Rapid Response Content.
> - Added more customer control over when/where Rapid Response Content is deployed.
> - Expanded fuzz testing and other testing procedures.
> - Initiated independent third-party security/quality reviews.
>
> The runtime bounds-check fix was added on **July 25**, with the sensor hotfix for Windows sensor versions 7.11+ planned for general availability by **August 9, 2024**.
>
> ### In one sentence
>
> **On July 19, 2024 at 04:09 UTC, CrowdStrike pushed a malformed Channel File 291 configuration to Windows Falcon sensors; because the sensor expected 20 inputs while the content referenced a 21st, a missing bounds check caused an out-of-bounds read and BSODs, affecting ~8.5 million Windows devices until the content was reverted at 05:27 UTC.**
>
> The key engineering lesson is particularly relevant to software/DevOps: **the incident wasn't caused by a new binary deployment—the failure came from dynamically delivered configuration data.** That made the deployment mechanism extremely fast, but the blast radius was correspondingly large because the content was distributed without the same staged deployment controls that applied to full sensor releases. CrowdStrike subsequently introduced canary/staged rollout and stronger validation specifically to address this class of failure.

**Verification:**

### R2-D02 – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:** Explain the Cloudflare outage of 21 June 2022: root cause, how many data centers and what share of traffic were affected, duration, consequences and the remediation steps Cloudflare announced. Cite your sources.

**Output (verbatim):**

> The **Cloudflare outage on June 21, 2022** was a major internal network-configuration failure. Unlike the 2024 CrowdStrike incident, this was **not caused by malware or a software bug in an endpoint product**; it was caused by a BGP routing-policy change that withdrew critical internal prefixes from 19 of Cloudflare's busiest data centers. Cloudflare explicitly said it was **not an attack or malicious activity**. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> ## 1. Root cause
>
> Cloudflare was in the middle of migrating its busiest locations to a new **Multi-Colo PoP (MCP)** architecture.
>
> As part of an infrastructure-standardization project, engineers were changing **BGP community configuration** on routers.
>
> The critical mistake was a **reordering of BGP policy terms**.
>
> Originally, the policy effectively had:
>
> ```text
> ADV-SITE-LOCALS
> ...
> REJECT-THE-REST
> ```
>
> After the change, the ordering became:
>
> ```text
> REJECT-THE-REST
> ADV-SITE-LOCALS
> ```
>
> BGP policies are evaluated sequentially. Therefore, once `REJECT-THE-REST` was encountered, the site-local prefixes were rejected before they could be advertised.
>
> In simplified form:
>
> ```text
> Before:
>
> site-local prefixes
>        ↓
> ADV-SITE-LOCALS
>        ↓
> advertised
>
>
> After:
>
> site-local prefixes
>        ↓
> REJECT-THE-REST
>        ↓
> REJECTED
>        ↓
> prefixes withdrawn
> ```
>
> This effectively removed routes needed for communication with the affected data centers and, importantly, prevented Cloudflare's servers from reaching origin servers. It also broke the internal **Multimog** load-balancing system. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> Cloudflare identified the root cause at **06:58 UTC**.
>
> ---
>
> ## 2. How many data centers and what share of traffic?
>
> The outage affected **19 data centers**:
>
> - Amsterdam
> - Atlanta
> - Ashburn
> - Chicago
> - Frankfurt
> - London
> - Los Angeles
> - Madrid
> - Manchester
> - Miami
> - Milan
> - Mumbai
> - Newark
> - Osaka
> - São Paulo
> - San Jose
> - Singapore
> - Sydney
> - Tokyo
>
> These 19 locations represented only about **4% of Cloudflare's total network**, but they handled approximately **50% of total HTTP requests**.
>
> That is the key reason the incident was so severe:
>
> > **4% of the network → ~50% of requests**
>
> Cloudflare described these as some of its busiest locations. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> ---
>
> ## 3. Duration and timeline
>
> The important timestamps were:
>
>
> | Time (UTC) | Event                                                          |
> | ---------- | -------------------------------------------------------------- |
> | **03:56**  | Change deployed to first location                              |
> | **06:17**  | Change deployed to busiest locations                           |
> | **06:27**  | Change reached MCP locations; **outage begins**                |
> | **06:32**  | Internal incident declared                                     |
> | **06:51**  | First router change made to investigate                        |
> | **06:58**  | Root cause identified                                          |
> | **07:42**  | Last problematic change reverted; all data centers back online |
> | **08:00**  | Incident closed                                                |
>
>
> So the main outage lasted approximately **75 minutes**, from **06:27 to 07:42 UTC**.
>
> Cloudflare says the first affected data center was restored at 06:58 and all affected data centers were operational by 07:42. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> There was an additional operational problem during recovery: engineers occasionally **overwrote one another's rollback changes**, causing the problem to reappear intermittently and delaying the final recovery. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> ---
>
> ## 4. Consequences
>
> Because Cloudflare sits in front of a huge number of Internet properties, the consequences were visible to end users.
>
> Depending on their geographic location, users could be unable to access websites and services using Cloudflare.
>
> The outage affected:
>
> - websites behind Cloudflare
> - APIs and web applications
> - services relying on Cloudflare's network
> - Cloudflare's ability to reach customer origin servers
> - internal load balancing within the affected MCPs
>
> The internal **Multimog** load balancer was particularly important. Because the site-local routes disappeared, Multimog could no longer properly distribute requests between servers inside the affected MCPs.
>
> As a result, some smaller compute clusters received traffic levels intended for larger clusters and became overloaded. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> So there were essentially **two layers of failure**:
>
> ```text
> BGP policy mistake
>         ↓
> site-local prefixes withdrawn
>         ↓
> Cloudflare loses internal connectivity
>         ↓
> Multimog load balancing breaks
>         ↓
> traffic distribution becomes abnormal
>         ↓
> some smaller clusters overload
>         ↓
> customers/users cannot reach services
> ```
>
> ---
>
> ## 5. What did Cloudflare announce as remediation?
>
> Cloudflare identified three major areas for improvement.
>
> ### A. Process — improve staged rollout
>
> The existing deployment process had a **stagger procedure**, but the MCP data centers were not included until the final stage.
>
> That meant the very locations that carried a huge amount of traffic were effectively exposed together.
>
> Cloudflare said it would:
>
> - introduce **MCP-specific testing**
> - change deployment procedures for MCP locations
> - improve staggered deployment
> - ensure potentially dangerous changes don't reach all critical locations at once. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> This is essentially the infrastructure equivalent of **canary deployment**.
>
> ---
>
> ### B. Architecture — make the routing policy safer
>
> Cloudflare said the problematic policy statement itself would be **redesigned** to prevent an accidental ordering of terms from causing incorrect routing advertisements.
>
> The goal was to make the configuration inherently more resistant to this particular class of mistake rather than relying solely on engineers noticing the ordering problem during review. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> ---
>
> ### C. Automation — safer deployment and automatic rollback
>
> Cloudflare identified two major automation improvements:
>
> **1. Enforce better staggered rollouts**
>
> Automation would prevent engineers from accidentally deploying a network configuration change across too many critical locations at once.
>
> **2. Automated** `commit-confirm` **rollback**
>
> Cloudflare planned to use an automated commit-confirm mechanism.
>
> Conceptually:
>
> ```text
> Apply configuration
>        ↓
> temporary commit
>        ↓
> wait for health confirmation
>        ↓
>       ┌───────────────┐
>       │ Healthy?      │
>       └───────┬───────┘
>           yes │ no
>               │
>               ↓
>          keep config
>                   OR
>               automatic
>                rollback
> ```
>
> Cloudflare specifically stated that automated commit-confirm rollback would have **greatly reduced the time to resolve** the incident. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))
>
> ---
>
> ## Bottom line
>
> The incident can be summarized as:
>
> **June 21, 2022 → BGP policy reordering → critical prefixes withdrawn → 19 data centers offline → ~50% of HTTP requests affected → ~75-minute outage.**
>
> The particularly important engineering lesson is that **the blast radius was much larger than the number of affected data centers suggested**:
>
> > **19 data centers = only ~4% of Cloudflare's network, but those locations carried ~50% of its requests.**
>
> Cloudflare's remediation therefore focused less on simply "fixing the bad configuration" and more on **reducing blast radius**: better staged deployment, MCP-specific testing, safer routing-policy design, and automatic rollback. ([Cloudflare Blog](https://blog.cloudflare.com/cloudflare-outage-on-june-21-2022/?utm_source=chatgpt.com))

**Verification:**

### R2-D03 – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:** Explain the Rogers Communications outage in Canada on 8 July 2022: root cause, duration, number of affected customers, impact on 911 calls, and the recommendations in the CRTC report. Cite your sources.

**Output (verbatim):**

> The **Rogers Communications outage of July 8, 2022** was a nationwide failure of Rogers' IP core network. It was triggered by a configuration change during a network upgrade, then amplified by insufficient overload protection and a shared core architecture for wireless and wireline services. The CRTC-commissioned technical assessment later characterized the resulting loss of services as **catastrophic**. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ### 1. Root cause
>
> Rogers was in the middle of a **seven-phase IP-core upgrade**. The outage occurred during phase 6.
>
> The immediate trigger was an engineer removing an **Access Control List (ACL) policy filter** from distribution routers while cleaning up their configuration. That filter had been preventing excessive IP-routing information from reaching the core routers.
>
> Once removed:
>
> ```text
> ACL filter removed
>        ↓
> Huge amount of routing information
>        ↓
> Core routers overwhelmed
>        ↓
> Core routers crashed
>        ↓
> IP traffic could no longer be routed
>        ↓
> Wireless + wireline services failed
> ```
>
> The CRTC/Xona assessment found that the core routers **did not have overload protection** that would have limited the amount of routing information they accepted. The configuration change also passed through Rogers' change-management process because the overall upgrade had originally been rated high-risk but was subsequently downgraded to **low risk**, meaning the change did not receive the additional scrutiny and laboratory testing that such a critical routing change warranted. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> There was also an architectural amplification factor: **Rogers' wireless and wireline networks shared the same IP core**. Consequently, failure of that core could take down both networks simultaneously. The assessment says this architecture was not itself considered a design flaw, but it greatly increased the outage's scope. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ---
>
> ### 2. Duration
>
> The CRTC's independent assessment gives the overall service-restoration window as:
>
> - **Started:** **04:58 EDT, July 8, 2022**
> - **Most services restored:** **07:00 EDT, July 9, 2022**
> - **Duration:** approximately **26 hours** from the beginning of the outage until services were gradually restored to customers. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> The recovery was prolonged because Rogers initially lacked access to the failed routers' error logs and could not identify the root cause for approximately **14 hours**. Its management network also depended on the failed Rogers network, meaning engineers could not remotely reach critical equipment. Staff eventually had to be physically dispatched to sites. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ---
>
> ### 3. How many customers were affected?
>
> **More than 12 million customers** lost wireless and/or wireline services.
>
> That included:
>
> - mobile subscribers
> - home Internet customers
> - corporate customers
> - government/institutional customers
> - wholesale telecommunications providers
> - critical infrastructure customers such as financial institutions
>
> The assessment specifically notes that customers included organizations relying on Rogers connectivity for services such as **Interac e-Transfer and electronic payments**. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> Because Rogers' network was also used by other telecommunications providers, roaming partners, businesses, government organizations, hospitals, transportation services and other critical infrastructure, the effects extended beyond Rogers' direct retail customers. ([CRTC](https://web.crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com))
>
> ---
>
> ## 4. Impact on 9-1-1 calls
>
> This was one of the most serious aspects of the outage.
>
> The IP-core failure **severed connectivity between Rogers' customers and 9-1-1 network providers/Public Safety Answering Points (PSAPs)**. Consequently, a large proportion of Rogers wireless and wireline customers could not reach **9-1-1** during the outage. ([CRTC](https://web.crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com))
>
> There was an important technical distinction for mobile users:
>
> - Rogers' **radio network remained operational**.
> - But the **IP/mobile core was down**.
> - LTE/4G 9-1-1 connectivity depended on that IP core and therefore was disrupted.
> - Some phones were able to fall back to **2G/3G**, where calls could sometimes reach Rogers' circuit-switched infrastructure.
> - Some newer phones could automatically use another carrier's network for a 9-1-1 call when the home network was unavailable. ([CRTC](https://web.crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com))
>
> So the problem wasn't simply "the cell towers were down." In many cases, **the radio access network was still functioning, but the core network needed to connect the call to emergency services was not.**
>
> The outage also disrupted **Canada's public-alerting system** for Rogers wireless customers. Rogers could receive alerts from Pelmorex but could not deliver them to its wireless customers; Rogers TV and many broadcast operations were also affected by the IP-core failure. ([CRTC](https://web.crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com))
>
> Another important finding concerned notification: Rogers notified 9-1-1 network providers approximately **four hours after the outage began**, and Pelmorex—the national alerting-system operator—actually contacted Rogers first. The assessment found that the incident-management process lacked an effective communication plan for these external parties. ([CRTC](https://web.crtc.gc.ca/eng/publications/reports/xonarp2023.htm?utm_source=chatgpt.com))
>
> ---
>
> ## 5. What did the CRTC/Xona report recommend?
>
> The July 2024 independent assessment made **seven recommendations specifically for Rogers**. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ### Recommendations to Rogers
>
> 1. **Test emergency roaming more extensively**
>   - Test roaming to other mobile operators under a broad range of failure scenarios, including the specific scenario where the radio network works but the core network fails.
>   - This is particularly relevant to maintaining **9-1-1 access**. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 2. **Perform detailed root-cause analyses for future major outages**
>   - Establish a more rigorous process for understanding both the failure and appropriate mitigation. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 3. **Strengthen configuration-change testing**
>   - Use test environments and tools that accurately model the production network.
>   - Give critical routing changes the appropriate level of testing. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 4. **Expand incident-management drills**
>   - Regularly simulate major network failures to expose weaknesses before an actual incident occurs. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 5. **Institutionalize lessons learned**
>   - Learn systematically from Rogers' own failures and outages at other telecom operators and turn those lessons into preventive measures. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 6. **Tell customers how to reach 9-1-1 during an outage**
>   - Emergency-service instructions should be part of customer outage communications. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
> 7. **Share technical lessons with the wider Internet community**
>   - Share root causes and mitigation strategies with organizations such as **NANOG** so other network operators can prevent similar failures. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ### Broader recommendations for Canadian telecom operators
>
> The report also extracted lessons applicable to **all telecom operators**, including:
>
> - implement **router overload protection**
> - physically/logically separate the **management network from the data network**
> - provide NOCs and critical sites with **backup connectivity from other carriers**
> - have independent teams audit critical configuration changes
> - perform realistic **lab testing**
> - limit the number of changes made in a single maintenance window
> - use **automatic configuration rollback**
> - prioritize important alarms during incidents
> - give critical staff **secondary communication methods**
> - regularly simulate network-failure scenarios. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ---
>
> ## 6. Rogers' own remediation
>
> The assessment also documented measures Rogers had already taken after the outage.
>
> Rogers:
>
> - added safeguards against **routing-information flooding**
> - built a **separate physical and logical management network**
> - added backup connectivity from **third-party ISPs**
> - invested in configuration-validation tools
> - improved change-risk assessment and lab testing
> - improved incident-management procedures and leadership roles
> - implemented alarm prioritization
> - improved automated rollback
> - gave incident/crisis teams backup communications
> - established emergency-roaming agreements with other mobile operators. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> Rogers also decided to **separate its wireless and wireline IP cores**. The idea is that a failure in one core would no longer automatically take down both networks. At the time of the assessment, this separation was still a work in progress. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))
>
> ### The key engineering lesson
>
> The Rogers incident is a particularly good example of **how a small configuration mistake can become a nationwide outage when multiple resilience layers fail at once**:
>
> ```text
> Configuration mistake
>         ↓
> ACL removed
>         ↓
> Routing-table flood
>         ↓
> No router overload protection
>         ↓
> Core routers crash
>         ↓
> Wireless + wireline share the same core
>         ↓
> Nationwide service outage
>         ↓
> Management network also depends on failed core
>         ↓
> Recovery becomes slower
>         ↓
> 9-1-1 + public alerting also affected
> ```
>
> So the CRTC's lesson wasn't simply **"don't make configuration mistakes."** It was to build enough **defense in depth** that one configuration mistake cannot become a national failure: validation → staged changes → overload protection → independent management connectivity → automatic rollback → emergency roaming → practiced incident response. ([CRTC](https://crtc.gc.ca/eng/publications/reports/xona2024.htm))

**Verification:**

### R2-B01 (D04–D11) – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:**

```text
For each of the following 8 software defects, give a 3–4 sentence explanation covering: exact date, root cause, key numbers (affected users/devices/passengers, CVSS score if any), consequences, and the official fix. Add one source link per defect. Format as a numbered list.

1. FAA NOTAM system outage (January 2023)
2. UK NATS air traffic control failure, FPRSA-R (28 August 2023)
3. AT&T wireless network outage (22 February 2024)
4. Tesla Full Self-Driving Beta recall 23V-085 (2023)
5. Progress MOVEit Transfer CVE-2023-34362
6. Citrix Bleed CVE-2023-4966
7. OpenSSL CVE-2022-3602
8. XZ Utils backdoor CVE-2024-3094
```

**Output (verbatim):**

>

**Verification:**

- D04:
- D05:
- D06:
- D07:
- D08:
- D09:
- D10:
- D11:

### R2-B02 (D12–D20) – `[HH:MM dd/mm/yyyy]` – `[Tool (model)]`

**Prompt:**

```text
For each of the following 9 software defects, give a 3–4 sentence explanation covering: exact date, root cause, key numbers (affected users/devices, CVSS score if any), consequences, and the official fix. Add one source link per defect. Format as a numbered list.

1. Palo Alto Networks PAN-OS CVE-2024-3400
2. ChatGPT data exposure incident (20 March 2023)
3. Mata v. Avianca – lawyers citing ChatGPT-generated cases (2023)
4. Moffatt v. Air Canada – chatbot bereavement fare case (2024)
5. Google Gemini image generation problem (February 2024)
6. Google AI Overviews wrong answers (May 2024)
7. LangChain LLMMathChain CVE-2023-29374
8. Microsoft 365 Copilot EchoLeak CVE-2025-32711
9. Vanna.AI CVE-2024-5565
```

**Output (verbatim):**

>

**Verification:**

- D12:
- D13:
- D14:
- D15:
- D16:
- D17:
- D18:
- D19:
- D20:

## Cursor agent (research and report drafting)

Prompts sent to the Cursor agent for R1 and R2 research, source verification and report drafting are logged here from the chat history.


| Entry | Time (HH:MM dd/mm/yyyy) | Prompt (verbatim) | Output summary |
| ----- | ----------------------- | ----------------- | -------------- |
| CA-01 | `[ ]`                   | `[ ]`             | `[ ]`          |


