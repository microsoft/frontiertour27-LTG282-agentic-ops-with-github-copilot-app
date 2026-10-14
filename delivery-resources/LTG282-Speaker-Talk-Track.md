# LTG282 – Caldova Waypoint On-Call Demo: Speaker Talk Track

> **Session type:** Lightning talk (13 minutes)
> **Format:** 4 setup slides → 6 recorded demo videos → closing
> **Tooling featured:** GitHub Copilot app + Azure MCP server, Azure Monitor, Azure Arc, Azure Copilot Observability Agent

---

## How to use this talk track

| Segment | Your role on stage |
|---|---|
| Slides 1–3 | Technical presenter addressing the audience |
| Slide 4 | Brief transition into the on-call role |
| Videos 1–6 | First-person on-call story, including the bonus investigation |
| Closing | Step out of the role and address the audience again |

- **Role labels and other notes are FYI only.** They provide context and extra information; they aren't meant to be read aloud.
- **Six recorded videos run beneath your narration.** Suggested compressed time segments and possible extra explanation time are labeled on screen.
- **Rehearse with the videos.** Run through the full track and decide where it's natural for *you* to pause a video, explain more, then resume.
- **No live Azure operations or issue submissions are required (or possible)** because of time constraints.

**Legend**

- **PRESENTER** – spoken to the audience as yourself
- **ON-CALL ADMIN** – spoken in first person as the on-call operator
- **PROMPT** – the prompt shown in the recording (don't read verbatim unless you want to)
- **APPROVAL** – the approval response shown in the recording
- **ACTION / EVIDENCE** – stage and production direction (not spoken)

---

## Part 1 – Four-slide setup | 00:00–02:00

### Slide 1 | Beginning the agentic operations journey

**PRESENTER**

All right, let's look at the concept of agentic operations using the "GitHub Copilot app" from an infrastructure perspective. If you support applications you didn't write and aren't involved in the CI/CD development and deployment process, this is probably familiar territory. You know the application, but not intimately: not every dependency, every setting, or every person who remembers why it's there. You're just here to make sure it keeps running. Today we'll follow an on-call scenario and use some agentic operations tools to figure out where an agent can help, while the technical decisions still belong to YOU – the operator.

### Slide 2 | The familiar firefight

**PRESENTER**

Think about the traditional firefight: check symptoms, diagnose, document, share, then act. You move between portals and write Kusto queries in Log Analytics, pulling together evidence and adding in the tribal knowledge. The domain expert isn't always beside you, and tribal knowledge doesn't necessarily answer the phone. This isn't about replacing the admin. It's about practical help finding and understanding evidence before making a change.

### Slide 3 | Copilot app plus Azure MCP

**PRESENTER**

The agentic tooling for this talk is the "GitHub Copilot app" connected to the Azure MCP server, authenticated with your signed-in credentials against the subscription. Your permissions constrain access across services such as Key Vault, networking, storage, and hybrid compute. Prompts set workflow boundaries; identity and permissions enforce access while following RBAC, governance, and policies. You set up the approval gates with AI for when read-only needs to become write access. Agentic operations is about assisting and augmenting YOUR domain expertise – not unleashing AI agents with autonomy and complete administrative access.

### Slide 4 | Transition into the on-call role

**TRANSITION TO "ON-CALL" PERSONA**

Let's dive into this. I'm on call for the Caldova Waypoint app. I know the app, but I wasn't involved in developing or implementing it. Besides making sure the front end is working as expected, I'm responsible for the back-end evidence-submission path via direct API calls from other processes – even a hybrid-connected box running in a satellite office. My shift was going pretty well… then this lands in my inbox.

---

## Part 2 – Six recorded demo videos

### Video 1 | Signal | 02:00–03:25

**Recording:** [D1 – Find the fire](demo-videos/D1-Find-the-fire.mp4)

**ACTION / EVIDENCE**
Play recorded video 1 – be prepared to start and stop as required. Show the Sev1 Azure Monitor email, then Copilot chat and subscription/Monitor/query discovery. Keep alert and query windows readable. Label: *Recorded demo — query waits compressed.*

**PROMPT**

> The wpdemo-5xx-spike alert fired for my Waypoint app in rg-waypoint-demo-ops. Using only Azure Monitor data, tell me what's failing, when it started, and the impact. Read-only, no fixes yet. Just triage for now.

**ON-CALL ADMIN**

Severity one. Azure Monitor is telling me about elevated HTTP 500 errors. All right, I need to understand what's failing before I reach for a fix. I give GHCP the alert and ask for Monitor data only: the failing path, when it started, and the impact. Read only. No changes. It finds the subscription and monitoring context and runs the queries. I don't have every resource name in my head, and I don't need to pretend I do. I need evidence I can follow, not a confident guess with a helpful tone.

The results have 500s mixed with 200s. Some requests get through, but that doesn't clear the back end. I check the onset in the query results and follow the window forward. The failures continue for about ten minutes, with no recovery showing up. I'm not comfortable dismissing that as just noise. The evidence-submission path is affected, and now I have a time window to work from. The alert has my attention; the query results give me somewhere useful to go next.

---

### Video 2 | Cause | 03:25–04:50

**Recording:** [D2 – What changed](demo-videos/D2-What-changed.mp4)

**ACTION / EVIDENCE**
Play recorded video 2. Show confidence-ranked findings, the Activity Log change timeline, and live Key Vault public-network-access setting changes alongside failure onset. Label compressed investigation waits; leave the evidence frames legible.

**PROMPT**

> Now find the root cause. Check the Activity Log for changes in rg-waypoint-demo-ops around when the errors started, and compare them to the live config of the app and its dependencies. Read-only, no fixes yet.

**ON-CALL ADMIN**

What changed? I ask Copilot to check the Activity Log around the failure window and compare those changes with the current app and dependency configuration. Still read only. I don't want to change something just because it appears near the top of a list. The findings are ranked by confidence, so I start there, then follow the evidence underneath. I need the timeline and the actual settings to agree. A convincing paragraph won't get the service back; knowing which dependency changed gives me a chance.

There it is: public network access to Key Vault was disabled, then the HTTP 500s start. This application's approved connectivity path depends on that access. The timeline and configuration support it as the root cause to address. That's much better than my working theory of Azure having a bad day. I know the setting, the dependency, and the scope. Now I need a recovery proposal that restores that path without changing anything else along the way.

---

### Video 3 | Recovery | 04:50–06:45

**Recording:** [D3 – Fix it, for real](demo-videos/D3-Fix-it-for-real.mp4)

**ACTION**
Show the reviewed resource and the exact proposed public-network-access setting before approval. Preserve existing authentication, authorization, and firewall restrictions. This is restoration of the approved demo architecture, **not** blanket public-access guidance. Play the approved change, then the recorded Evidence endpoint checks.

**PROMPT**

> Recommend the smallest fix that restores service, and show me the exact change before making it. Don't change anything until I approve.

**ON-CALL ADMIN**

Before I touch anything, I want to know the exact change. I ask for the smallest fix and tell it not to do anything until I give it the go-ahead. That way I can review the proposed plan, the targeted resource, and the settings. This should restore public connectivity for the existing approved architecture; authentication, authorization, and the existing network restrictions stay in place. I'm not authorizing any substantial changes to the subscription or configuration. The proposal fits with the investigation we just did, so I approve that specific change. Then I level up and ask for fresh checks against the failing path to see if things worked.

**APPROVAL**

> Approved. Apply it and confirm the 5xx errors stop.

**ON-CALL ADMIN**

The change is applied, and it checks the Evidence endpoint instead of assuming the alert has gone quiet for a good reason. All the requests checked out OK after the change and return HTTP 200s. It follows the results across the observation window and checks the time range, not just the last green response. That gives me confidence and some recovery evidence that the fix worked. It doesn't guarantee every future request, but it's enough to move this investigation forward.

**ACTION / EVIDENCE**
Overlay: *Recorded verification — five-minute observation window compressed.* Retain start/end timestamps and checked-request results. Do not invent counts or claim universal future recovery. End this clip on the observed recovery, then transition to hybrid.

---

### Video 4 | Hybrid | 06:45–08:30

**Recording:** [D4 – Not just cloud](demo-videos/D4-Not-just-cloud.mp4)

**ACTION**
Play recorded video 4 for waypoint-hybrid-host in rg-waypoint-demo-hybrid, simulating an on-premises box through Azure Arc. Show the connected host, configured syslog in Log Analytics, the administrative stop and clean stop ten seconds later, then the approved remote command and verification.

**PROMPT**

> Check the Arc machine waypoint-hybrid-host in rg-waypoint-demo-hybrid. Is it connected, healthy, and are its services running? If anything's wrong, tell me why and recommend a fix. Don't change anything until I approve.

**ON-CALL ADMIN**

The cloud side looks better. But I should check on that hybrid VM back at the remote office. I check waypoint-hybrid-host through Azure Arc. It's connected and looks healthy at the host level, but I still need to know whether the Forwarder service is working. Syslog collection is configured with Azure Arc, so those logs will be in Log Analytics. The Waypoint Forwarder service is stopped. The sequence is specific: an administrative stop, then a clean stop ten seconds later. This isn't evidence of a crash – it was a manual intervention by someone. I don't need to guess who did it or why; I need to understand what stopped.

**APPROVAL** *(for context only – a simple approval response on screen)*

> Approve only the reviewed start of the Waypoint Forwarder service on waypoint-hybrid-host in rg-waypoint-demo-hybrid using the proposed Arc remote command. Then verify service state and the forwarding/application path.

**ON-CALL ADMIN**

I review the proposed start for that service on that host before I approve it. The command goes through Azure Arc, and I ask it to check the service state and the forwarding/application path. The service is running, and the path returns HTTP 200. That's the evidence I was looking for beyond the simple "connected" badge in the portal. Now we've checked the cloud dependency and the hybrid service separately. I can breathe a little easier, but I don't want the next on-call admin to inherit exactly the same surprise. I ask for a prevention plan, not another change.

---

### Video 5 | Prevention | 08:30–10:05

**Recording:** [D5 – Never again at 3AM](demo-videos/D5-Never-again-at-3AM.mp4)

**ACTION / EVIDENCE**
Play recorded video 5 and show only the top recommendation per issue, before the bonus investigation.

**PROMPT**

> Recommend an automated way to detect and fix both of today's issues so they don't happen again. Use Azure-native tools only. Show me the plan first. Don't build anything until I approve. Keep it to the top recommendation for each issue.

**ON-CALL ADMIN**

I keep the request small: the top Azure-native recommendation for each issue. Build me a plan first, but don't actually build anything or make any changes. For Key Vault, I want a guardrail that detects a regression from the approved access path, with restoration only under reviewed authorization. It has to be scoped to this architecture and this resource, not every vault in sight. I need something the team can inspect and test. We can investigate re-architecting network access using more secure private endpoints at a later date.

For the Forwarder, review a log alert for missing expected service heartbeat or forwarding records, not just the host heartbeat. The proposed approved runbook inspects through Arc Run Command, starts the service if appropriate, and verifies it about sixty seconds after the command. I keep that verification delay separate from the detection threshold, which still needs configuration and testing. Before adopting either plan, we should use managed identities with narrow scope, resource and service allowlists, and an audit trail. Intentional maintenance can't become an automatic restart. I leave both recommendations as a plan I can discuss with the team during regular business hours.

---

### Video 6 | Bonus: Observability investigation and issue | 10:05–11:40

**Recording:** [Bonus – Azure Copilot Observability Agent](demo-videos/D-BONUS-Azure-Copilot-Observability-Agent.mp4)

**ACTION**
Remain in the on-call role throughout the bonus. Play recorded video 6. From the original email, open **Investigate with an agent** in the authenticated Azure portal. Verify the displayed range begins two hours before the impact alert. Start the investigation; compress collection waits. Review findings, supporting services, chat, graphs, charts, and recommendations. Use **Create issue** only in the recording; show confirmation only if visible. The spoken handoff describes the reviewed issue workflow, not an unverified successful submission. No Teams integration or Microsoft support-case claim.

**ON-CALL ADMIN**

I want to leave the next shift something useful about everything that took place with this incident. If I go back to the original alert email and open "Investigate with an agent" in the Azure portal, the Azure Copilot Observability Agent gives me another way to gather all sorts of incident evidence. It proposes the investigation range: two hours before the impact alert. We want that lead-in, not just the moment the errors appear. Once the findings arrive, you can work through the supporting services, chat, graphs, charts, and recommendations.

After reviewing the investigation, there's a "Create issue" option for the incident handoff. It keeps the supporting information and chat together for the team, rather than leaving my chicken-scratch notes on paper or random thoughts in a text file and hoping somebody decodes them. This becomes an incident issue in the investigation workspace, not a Microsoft support case. The next shift needs a usable account, not just another number.

---

## Part 3 – Closing | Return to technical presenter | 11:40–13:00

**PRESENTER**

All right – what should you take back to your infrastructure work? The GitHub Copilot app with Azure MCP can help assemble evidence under authorized credentials, but the operator still owns the decisions. Remember to set up prompts with "read and investigate first." This lets you review a narrow change, approve it, then verify the outcome on the affected path. The big thing here is that you're in control, and the agent acts within the scope and boundaries of your account and under the same governance, policy, and RBAC controls that are already in place. You are the human in the middle before changes get made.

Use the GitHub repository shown on screen to explore the session materials and demo setup. You don't have to automate everything on day one. Pick one practical investigation, learn what the tools can show you, and work outward from there. Thank you.

**ACTION**
Show the session GitHub repository link supplied for the presentation. No URL is supplied in this script; confirm the on-screen destination and available materials before delivery. Do not promise a published recording that hasn't been verified.

---

## Backstage production notes

### Timing and video production

- Run through this script and adapt the words and timing so that YOU sound natural.
- The goal: you have the core talk track and talking points, supported by recorded demos that you start and stop as needed to fit the time allocation.
- Your talk track is designed to run over the top of videos that you control.
- The timings below are rehearsal/edit budgets, not measured clip lengths. Keep the existing windows and trim the talk track to fit.

### 13-minute run of show

| Segment / window | Words | Narration | Other time | Total |
|---|---:|---:|---:|---:|
| Four slides \| 00:00–02:00 | 245 | 1:41 | 0:19 | 2:00 |
| Video 1: Signal \| 02:00–03:25 | 170 | 1:10 | 0:15 | 1:25 |
| Video 2: Cause \| 03:25–04:50 | 172 | 1:11 | 0:14 | 1:25 |
| Video 3: Recovery \| 04:50–06:45 | 183 | 1:16 | 0:39 | 1:55 |
| Video 4: Hybrid \| 06:45–08:30 | 185 | 1:17 | 0:28 | 1:45 |
| Video 5: Prevention \| 08:30–10:05 | 183 | 1:16 | 0:19 | 1:35 |
| Video 6: Bonus \| 10:05–11:40 | 188 | 1:18 | 0:17 | 1:35 |
| Closing \| 11:40–13:00 | 181 | 1:15 | 0:05 | 1:20 |
| **Total** | **1,507** | **10:24** | **2:36** | **13:00** |
