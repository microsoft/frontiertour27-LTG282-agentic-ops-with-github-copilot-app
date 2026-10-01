## Before you're done

This repo has been created for your AI Tour 2027 session. Here's how to get it ready.

**Easiest path — use the agent (recommended):**

- Open GitHub Copilot Chat and say `help me initialize repo`. The agent will walk you through getting the README populated.
- When you're ready to publish, say `help me finalize repo`. The agent will clean up unused folders, validate everything, and remove this "Before you're done" section and other extra stuff that attendees don't need to see.
- Curious how it works? Read the [agent workflow](.github/AGENT-WORKFLOW.md).

**Doing it manually?**

Fill in the sections below yourself, then:

- Delete any placeholder folders you don't need (`data/`, `infra/`, etc.)
- Delete this "Before you're done" section
- Delete `.github/agents/`, `.github/tests/`, `.github/copilot-instructions.md`, and `.github/AGENT-WORKFLOW.md` — these are template tooling, not part of your published repo

**Folder conventions:**

- Attendee step-by-step guidance goes in `instructions/`. If you use MkDocs or a docs site instead, put it in `docs/` and link to it from this README.
- Reference material and background reading go in `docs/`.
- Presenter notes, deck link, recordings, and re-delivery materials go in `delivery-resources/`. Fill in [`delivery-resources/README.md`](delivery-resources/README.md).
- You can add a `.devcontainer/` folder if needed.

---

<a name="start-building"></a>

<p align="center">
<img src="img/banner-ai-tour-27.png" alt="Microsoft AI Tour 2027" width="100%"/>
</p>

# [Microsoft AI Tour 2027](https://aitour.microsoft.com)

## 🔥 LTG282: Agentic Ops with GitHub Copilot App

### Session description

It's 3AM, prod is down, and the fix isn't a pull request. See the GitHub Copilot App use Azure, Arc & Log Analytics MCP servers to hunt config drift and repair your cloud and hybrid estate live—then automate the guardrail so it never happens again.

### 🚀 Getting started

#### In a guided session

If you're following along during a live session:

1. Watch the live demo as the GitHub Copilot App investigates and repairs the incident
2. Open the [session docs](docs/index.md) to follow along with the scenario and resources

#### On your own

If you're learning at your own pace:

1. Clone this repository
2. Follow the session guidance in the [session docs](docs/index.md)
3. Explore the sample code in [`src/`](src/README.md) and infrastructure in [`infra/`](infra/README.md)

### 🎯 Learning outcomes

By the end of this session, you will be able to:

- Use the GitHub Copilot App with Azure, Azure Arc, and Log Analytics MCP servers to investigate a live production incident across cloud and hybrid resources.
- Detect configuration drift and apply a targeted repair to your Azure and Arc-enabled estate directly from an agentic session.
- Turn the fix into an automated guardrail so the same drift is caught and prevented going forward.

### 💻 Technologies used

- GitHub Copilot App
- Azure MCP Server
- Azure Arc
- Azure Monitor Log Analytics
- Model Context Protocol (MCP)

### 📚 Continue your learning

Pick your next step based on your learning style:

| Resource | What you'll get |
|----------|-----------------|
| **[Microsoft Learn](https://learn.microsoft.com)** | Official documentation and guided learning paths on these topics |
| **[AI Tour 2027 Resource Center](https://aka.ms/aitour27-resource-center)** | Additional session repos and materials from AI Tour 2027 |
| **[Microsoft Foundry Community](https://aka.ms/MicrosoftFoundryDiscord-AITour27)** | Connect with other learners and experts in our Discord community |

### 🌟 Microsoft Learn MCP Server

<!-- Remove this section if the Microsoft Learn MCP Server is not relevant to the session. -->

The Microsoft Learn MCP Server gives your AI agent direct access to Microsoft's official documentation — grounded, up-to-date answers about the topics in this session.

**GitHub Copilot CLI** — Install with:

```shell
copilot plugin install microsoftdocs/mcp
```

**VS Code** — One-click install:  
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Microsoft_Learn_MCP-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=microsoft-learn&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Flearn.microsoft.com%2Fapi%2Fmcp%22%7D)

For more information, visit the [Learn MCP Server repo](https://aka.ms/learnmcp).

### 👥 Content owners

<table>
<tr>
    <td align="center"><a href="http://github.com/RicksterCDN">
        <img src="https://github.com/RicksterCDN.png" width="100px;" alt="Rick Claus"/><br />
        <sub><b>Rick Claus</b></sub></a><br />
            <a href="https://github.com/RicksterCDN" title="talk">📢</a>
    </td>
</tr></table>

### Deliver this session

Presenters and re-delivery partners can find the deck, recordings, presenter
notes, and delivery guidance in [`delivery-resources/`](delivery-resources/README.md).

### ⚖️ Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow [Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general). Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.

Any use of third-party trademarks or logos are subject to those third-party's policies.
