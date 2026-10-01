# Delivery resources

Presenter, re-delivery, and train-the-trainer materials for LTG282: Agentic Ops with GitHub Copilot App.

## Core materials

| Item | Link | Notes |
|---|---|---|
| Delivery deck | [LTG282 slides](https://aka.ms/aitour27/LTG282/slides/en) | Public deck |
| Session recording |  | Not yet available |
| Attendee landing page | [Session README](../README.md) | Public starting point |
| Session docs | [Session docs](../docs/README.md) | Attendee guidance entry point |

## Delivery checklist

- Review the session README
- Review the session docs
- Open the deck
- Review the presenter guidance below
- Review live demo reproducibility guidance
- Validate the GitHub Copilot App and MCP server setup before going on stage

## Session preparation

- Review the attendee entry point from the root README.
- Review the delivery deck.
- Confirm the GitHub Copilot App is signed in and the Azure, Azure Arc, and Log Analytics MCP servers are connected.
- Confirm access to the Azure subscription, Arc-enabled resources, and Log Analytics workspace used in the demo.

## Presenter notes

**Audience:** IT Pros and cloud/infrastructure engineers on hybrid Azure (roughly 70% broad IT Pro, 30% deep technical).

**The problem this talk solves:**

- IT Pros who run hybrid Azure estates (cloud + on-premises/Arc) still fight 3AM incidents with portal safaris, SSH hops, scattered Kusto tabs, and tribal knowledge.
- Most "Copilot for infrastructure" stories stop at writing or reviewing Infrastructure-as-Code pull requests — a Day-1, dev-centric view that leaves Day-2 operations (drift, misconfiguration, incident response, hybrid health) untouched.
- The gap: a single, governed place to find, diagnose, fix, and prevent infrastructure problems — one that can act on live infrastructure, not just propose code.

**Why the GitHub Copilot App is more than an IaC PR writer/reviewer:**

- The app is an agent-native desktop control center (Canvases, My Work, Automations, Agent Merge) that connects to MCP servers.
- Through Azure MCP, Azure Arc, and Azure Monitor / Log Analytics MCP, the app's ops agent reads *and* acts on the live estate: it can restore a network rule, remediate an Arc-connected server, and schedule a guardrail — directly in the subscription, with human approval and scoped permissions.
- That's the leap: from "open a PR and wait for a pipeline" to "fix the running system now, safely." Pull requests remain available when a code change is the right answer, but the app isn't limited to them.

**The governance boundary (the sharp point):**

- The demo runs on Caldova Waypoint — invoice assurance for contract manufacturing — which itself has governed agents that assist but never own the writes.
- Two boundaries, cleanly separated: Waypoint's agents make business decisions inside the system of record; the Copilot App's ops agent fixes the Azure infrastructure outside it. The ops fix never touches a case, a finding, or an approval.
- This pre-empts the top objection from regulated and enterprise audiences ("you're letting an agent change things?"): the ops agent is scoped to infrastructure, and the business system of record stays governed.

**Takeaways:** the Copilot App + MCP is a Day-2 operations control center; it acts on live cloud and hybrid infrastructure with governance; drift can be found, fixed, and prevented from one canvas.

**Call to action:** get the app ([gh.io/app](https://gh.io/app)); wire up Azure MCP, Azure Arc, and Azure Monitor.

## Run of show

One 3AM incident, five moves. Motif: an on-screen incident clock ticks from 03:00 (ON-CALL) to 03:42 (PAGER SILENT).

| Segment | Tooling | What happens | What it proves |
|---|---|---|---|
| Cold open (~2 min, talk) | — | The 3AM page: Waypoint is down. The old firefight vs. one governed canvas. | — |
| Act 1 · Find | Log Analytics MCP | A Kusto query pinpoints the failure spike on Waypoint. | Conversational diagnostics in one console (no five-tab Kusto safari). |
| Act 2 · Diagnose | Azure MCP | Live config plus the Activity Log reveal the drift — a network rule flipped. | Live drift detection against real Azure state; reasoning about why, not just what. |
| Act 3 · Fix live | Azure MCP (write) | The money shot: approve on the canvas; the agent restores the rule in Azure — no PR; Waypoint's writes stay governed. | The app acts on infrastructure — human-in-the-loop, scoped permissions; the governance boundary is preserved. |
| Act 4 · Hybrid | Azure Arc | Remediate the on-premises CMO evidence forwarder from the same canvas. | One pane of glass for cloud and hybrid. |
| Act 5 · Prevent | Automations + Azure Monitor | A guardrail that self-heals on drift, plus an evidence-rich runbook for the audit trail. | Agentic ops becomes durable prevention. |
| Close (~1 min, talk) | — | Beyond the PR — your Day-2 ops control center. gh.io/app; wire up Azure MCP + Arc + Monitor. | — |

<!-- TODO: Add timings for Acts 1–5 and transition notes. -->

## Demo reproducibility

This session includes a live demo on the Caldova Waypoint scenario: the GitHub Copilot App
uses the Log Analytics, Azure, and Azure Arc MCP servers to find and diagnose a flipped
network rule, restore it live with human approval, remediate an Arc-connected on-premises
evidence forwarder, and schedule a self-healing guardrail with Automations and Azure Monitor.
See the run of show above for the act-by-act flow.

<!-- TODO: Add the demo steps, environment details, and links to the code in ../src/ and infrastructure in ../infra/. -->

## Setup notes

- Sample code: [`src/`](../src/README.md)
- Infrastructure: [`infra/`](../infra/README.md)

## Support

Content owner or contact: Rick Claus ([@RicksterCDN](https://github.com/RicksterCDN))
