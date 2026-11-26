<p>
  <a href="https://withone.ai/knowledge">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/withoneai/knowledge/main/assets/banner-dark.svg">
      <img src="https://raw.githubusercontent.com/withoneai/knowledge/main/assets/banner-light.svg" alt="One Knowledge. The world's largest API knowledge base, built for agents." width="100%">
    </picture>
  </a>
</p>

<h3 align="center">One Knowledge</h3>

<p align="center">
  <a href="https://withone.ai/knowledge"><strong>API directory</strong></a>
  &nbsp;&middot;&nbsp;
  <a href="https://withone.ai/knowledge/how-to-use"><strong>How to use it</strong></a>
  &nbsp;&middot;&nbsp;
  <a href="https://withone.ai/docs"><strong>Docs</strong></a>
  &nbsp;&middot;&nbsp;
  <a href="https://withone.ai"><strong>Website</strong></a>
  &nbsp;&middot;&nbsp;
  <a href="https://app.withone.ai"><strong>Dashboard</strong></a>
  &nbsp;&middot;&nbsp;
  <a href="https://withone.ai/changelog"><strong>Changelog</strong></a>
</p>

<p align="center">
  <a href="https://withone.ai/knowledge"><img src="https://img.shields.io/endpoint?url=https%3A%2F%2Fapi.withone.ai%2Fopen%2Fcount%2Fplatforms&color=447D5D&labelColor=132A21&style=flat-square" alt="platforms"></a>
  &nbsp;
  <a href="https://withone.ai/knowledge"><img src="https://img.shields.io/endpoint?url=https%3A%2F%2Fapi.withone.ai%2Fopen%2Fcount%2Ftools&label=verified%20tools&color=447D5D&labelColor=132A21&style=flat-square" alt="verified tools"></a>
  &nbsp;
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-OKCL--1.0-447D5D?labelColor=132A21&style=flat-square" alt="License OKCL-1.0"></a>
</p>

Agents fail against real systems in predictable ways. Wrong parameters, invented endpoints, an API that changed on Tuesday. One Knowledge knows how each action works before the agent runs it. Every parameter, every auth flow, every edge case. Structured for machines and verified by&nbsp;humans.

Tools are tested before they are made available to agents. The knowledge is open source, so one fix reaches every agent, and this repo is its public home. Search an app and read its actions in the [API directory](https://withone.ai/knowledge), read the same knowledge over the [open API](#read-it-over-the-api), and open an issue here when something is wrong or&nbsp;missing.

## Use it from your agent

Point any MCP agent at One's hosted server and sign in when it&nbsp;asks.

```bash
claude mcp add --transport http one https://mcp.withone.ai/mcp
```

Or install the [One CLI](https://github.com/withoneai/cli) with `npm install -g @withone/cli` and run `one init`. Setup guides are at&nbsp;[withone.ai/mcp](https://withone.ai/mcp).

Every task then follows the same three steps. The second one returns the knowledge, with the required parameters and the validation&nbsp;rules.

```bash
# What am I connected to?
one list

# Which action, and how? Its knowledge comes back with it.
one actions find gmail "send an email"

# Do it, through your own connection.
one actions execute gmail <actionId> <connectionKey>
```

Over MCP the same steps are `list_one_integrations`, `find_one_actions` and&nbsp;`execute_one_action`.

## Read it over the API

The open API returns the same knowledge. Send a free [API key](https://app.withone.ai/settings/api-keys) in the `x-one-secret` header. The base URL is&nbsp;`https://api.withone.ai`.

| Endpoint | Returns |
|----------|---------|
| `GET /open/knowledge/:platform` | The platform's&nbsp;overview |
| `GET /open/knowledge/:platform/auth` | Its authentication&nbsp;details |
| `GET /open/knowledge/:platform/actions` | Its actions, paged with `page` (from 1) and `limit` (default 20, max&nbsp;150) |
| `GET /open/knowledge/:platform/actions/search?query=` | The actions that match, with an optional&nbsp;`limit` |
| `GET /open/knowledge/:platform/actions/:actionId` | One action's full&nbsp;knowledge |
| `GET /open/count/platforms` and `GET /open/count/tools` | Live counts as [shields.io](https://shields.io/badges/endpoint-badge) badge JSON. No key&nbsp;needed |

```bash
# Airtable's overview
curl 'https://api.withone.ai/open/knowledge/airtable' \
  --header 'x-one-secret: YOUR_ONE_API_KEY'

# Find an action, then read it by its id
curl 'https://api.withone.ai/open/knowledge/airtable/actions/search?query=list%20bases' \
  --header 'x-one-secret: YOUR_ONE_API_KEY'
curl 'https://api.withone.ai/open/knowledge/airtable/actions/ACTION_ID' \
  --header 'x-one-secret: YOUR_ONE_API_KEY'
```

Knowledge comes back as Markdown with YAML front matter, in a `markdown` field. An action list comes back as `{ rows, total, pages, page }`, and each row carries the action's `id`, `title`, `method` and `path`. Search returns the matching rows as an&nbsp;array.

## What is in an action

Every action is one Markdown document, and every document has the same&nbsp;parts.

| Part | What it&nbsp;holds |
|------|---------------|
| **Metadata** | YAML front matter with the platform, category, version, license, maintainer and the date it was last&nbsp;updated |
| **Authentication** | OAuth details, required credentials, scopes and token&nbsp;refresh |
| **Method, URL and&nbsp;headers** | The call itself, with its prerequisites and a&nbsp;description |
| **Parameters** | Required and optional path, query and body parameters, with types and&nbsp;descriptions |
| **Enforcement rules** | Constraints that keep a call correct, such as query against body, with valid and invalid&nbsp;examples |
| **Response** | The structure of each outcome, with field types and&nbsp;descriptions |
| **Examples** | A sample request and worked usage&nbsp;examples |
| **Behavior and&nbsp;notes** | What the call does step by step, and its limits and&nbsp;caveats |

## Fix something or request a&nbsp;platform

One maintains the knowledge, and one fix reaches every agent that reads it. If something is outdated, incorrect or missing, open an&nbsp;issue.

- [Report outdated or incorrect knowledge](../../issues/new?template=report-outdated-knowledge.yml) when an action's parameters, authentication or endpoint has&nbsp;changed
- [Request a new platform](../../issues/new?template=request-new-platform.yml) that the knowledge base does not cover&nbsp;yet

## License

One Knowledge is released under the [One Knowledge Commons License v1.0](./LICENSE) (OKCL-1.0). It is free to use, modify and distribute with attribution. It may not be used to build a competing knowledge base, and companies that sell integration or agent infrastructure and earn more than $1M a year need a commercial license. Read the [full text](./LICENSE) before you build on&nbsp;it.
