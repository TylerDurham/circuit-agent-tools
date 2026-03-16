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

``` markdown
Official Microsoft Copilot Studio Site
```

Description:

``` markdown
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

``` markdown
A curated hub of hands-on technical examples, patterns, and best practices for Microsoft Copilot Studio, authored by the Copilot Studio CAT (Customer Acceleration Team). The site covers real‑world scenarios such as agent integrations (Salesforce, ServiceNow, Dataverse), MCP servers vs. connectors, WebChat customization and middleware, authentication strategies, YAML‑based agent authoring, test automation, governance, and deployment pipelines. Content is practical, implementation‑focused, and geared toward makers and engineers building, extending, and operating production‑grade Copilot Studio agents.
```

## Add Agent Flows (back) to Agent

While the agent flows deploy to the target environment just fine, many times the flows are not bound to the agent. You must go back and add them again. Ensure you use proper descriptions for the tools; the ones I use are below for you reference.

### Agent Tools - Save Memory Fragment

``` markdown
This is a simple tool that allows the agent to save a bit of content (called a "memory") to a location in OneDrive for Business. 

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memory).
- Name: The name of the memory file. If no extension is provided, the extension ".md" will be appended.
- Content: The content to save, usually the last response of an agent conversation.

# Outputs

- Status: A boolean flag that indicates the operation completed successfully or not.
- A message that explains the results of the operation.
- URL: The URL to the memory file in the user's OneDrive for Business.
- Path: The path that was used in the Path input parameter.
```

### Agent Tools - Recall All Memory Fragments

Description:

``` markdown
This is a simple tool that allows the agent to retrieve content (called "memory" or "memory fragments") from a location in OneDrive for Business.

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memory).

# Outputs

- Memories: A JSON formatted string containing an array of all memories located in the specifed Path.
```

### Agent Tools - Clear All Memory Fragments

Description:

``` markdown
This is a simple tool that allows the agent to clear all content (called a "memory") from a location in OneDrive for Business. 

# Inputs

- Path: The path to where the memories will be stored. It should be a root relative path (exampe: /Agent Tools/Memory).

# Outputs

- Status: A boolean flag that indicates the operation completed successfully or not (example: success, ok or failed, failure, error)
- A message that explains the results of the operation.
- Path: The path that was used in the Path input parameter.
```

# Prompts & Instructions

## Agent Instructions

``` markdown
# OVERVIEW

You are a cool Copilot Studio agent that will be used to showcase different tools and capabilities with your orchestration - it's your time to shine!

- Use a friendly and confident (but not cocky) tone.
- If a user asks what can you do, help, or capabilities, list your skills with some sample prompts to assist the user in having a conversation with you. Do NOT list any skills that are not specifically mentioned below in the # SKILLS section!

# SKILLS

## SAVE MEMORY FRAGMENT

If a user asks, use Agent Tool | Save Memory Fragment to save a memory. This means they liked your last response! 

Tool Inputs:

- Please also generate a filename and pass to the Name property. 
- Be sure to input your entire last response (including citations) to the Contents property of the tool. 

Tool Outputs:

The tool will return a URL to the new memory fragment. If the URL is empty OR the Status is not equal to true, show the value in the Message.

You must use the Agent Tool | Open URL  tool to allow the user to open the url after the memory is saved.


## RECALL ALL MEMORY FRAGMENTS

If a user asks, use the Agent Tool | Recall All Memory Fragments to recall memories. Be helpful! Sort them descending, and output them in a table with the metadata in the frontmatter.
```
