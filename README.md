# Circuit Copilot Agent Tools

# Deployment

Grab the solution package.
Import into Copilot Studio

## Post Deployment

### Fix Knowledge Sources

Copilot Studio doesn't sometimes leaves Knowledge Sources out of the solution (I have no idea why).

There should be 3 knowledge sources. You can quickly recreate them by using the values below.

#### Official Microsoft Copilot Studio Learning Site

URL:

```url
https://learn.microsoft.com/en-us/microsoft-copilot-studio/
```

Name:

```name
Microsoft Copilot Studio
```

Description:

```description
Microsoft Copilot Studio documentation is an authoritative, end‑to‑end reference for building, extending, testing, and deploying AI agents and workflows in Copilot Studio. It provides structured guidance across core tasks (agent creation, topics, variables, prompts, tools/connectors, and knowledge sources like public websites/SharePoint/files), plus troubleshooting, release updates, training resources, and operational best practices (administration, analytics, publishing to channels such as Teams and websites). Use this site as the primary source of truth for Copilot Studio capabilities, recommended patterns, and current product guidance.
```

#### Official Microsoft Copilot Studio Site

URL:

```url
https://www.microsoft.com/en-us/microsoft-copilot
```

Name:

```name
Official Microsoft Copilot Studio Site
```

Description:

```description
The official Microsoft landing site for Copilot across organizations and personal use, providing an overview of Copilot capabilities, product options, licensing, privacy and security commitments, and common usage scenarios. It helps users understand what Copilots are, how different Copilot offerings compare, how Copilot integrates with Microsoft 365 apps (Word, Excel, PowerPoint, Teams), and where to find documentation, tutorials, and next steps. Designed as a discovery and onboarding resource rather than an implementation guide.
```

#### Copilot Studio CAT Team Blog

URL:

```url
https://learn.microsoft.com/en-us/microsoft-copilot-studio/
```

Name:

```name
Copilot Studio CAT Team Blog
```

Description:

```description
A curated hub of hands-on technical examples, patterns, and best practices for Microsoft Copilot Studio, authored by the Copilot Studio CAT (Customer Acceleration Team). The site covers real‑world scenarios such as agent integrations (Salesforce, ServiceNow, Dataverse), MCP servers vs. connectors, WebChat customization and middleware, authentication strategies, YAML‑based agent authoring, test automation, governance, and deployment pipelines. Content is practical, implementation‑focused, and geared toward makers and engineers building, extending, and operating production‑grade Copilot Studio agents.
```

## Add Agent Flows (back) to Agent

While the agent flows deploy to the target environment just fine, many times the flows are not bound to the agent. You must go back and add them again. Ensure you use proper descriptions for the tools; the ones I use are below for you reference.

### Agent Tools - Save Memory Fragment

``` text
This is a simple tool that allows the agent to save a bit of content (called a "memory") to a location in OneDrive for Business. 

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memories).
- Name: The name of the memory file. If no extension is provided, the extension ".md" will be appended.
- Content: The content to save, usually the last response of an agent conversation.

# Outputs

- Status: A boolean flag that indicates the operation completed successfully or not..
- URL: The URL to the memory file in the user's OneDrive for Business.
- A message that explains the results of the operation.
- Path: The path to the memory file in the user's OneDrive for Business.
```

### Agent Tools - Recall All Memory Fragments

Description:

```text
This is a simple tool that allows the agent to retrieve content (called a "memories") from a location in OneDrive for Business.

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memories).

# Outputs

- Memories: A JSON formatted string containing an array of all memories located in the specifed Path.
```

### Agent Tools - Clear All Memory Fragments

Description:

```text
This is a simple tool that allows the agent to clear all content (called a "memory") from a location in OneDrive for Business. 

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memories).

# Outputs

- Status: A boolean flag that indicates the operation completed successfully or not (example: success, ok or failed, failure, error)
- A message that explains the results of the operation.
- Path: The path that was used in the Path input parameter.
```

