<img src="https://assets.withone.ai/banners/knowledge.png?v=2" alt="One Knowledge — The world's largest open knowledge base for APIs." style="border-radius: 5px;">

<h3 align="center">One Knowledge</h3>
<p align="center">The world's largest API knowledge base, built for agents.</p>

<p align="center">
  <a href="https://withone.ai/knowledge"><strong>Browse Knowledge</strong></a>
  &nbsp;·&nbsp;
  <a href="https://withone.ai"><strong>Website</strong></a>
  &nbsp;·&nbsp;
  <a href="https://withone.ai/docs"><strong>Docs</strong></a>
  &nbsp;·&nbsp;
  <a href="https://app.withone.ai"><strong>Dashboard</strong></a>
  &nbsp;·&nbsp;
  <a href="https://withone.ai/changelog"><strong>Changelog</strong></a>
  &nbsp;·&nbsp;
  <a href="https://x.com/withoneai"><strong>X</strong></a>
  &nbsp;·&nbsp;
  <a href="https://linkedin.com/company/withoneai"><strong>LinkedIn</strong></a>
</p>

<p align="center">
  <a href="https://withone.ai/knowledge"><img src="https://img.shields.io/endpoint?url=https%3A%2F%2Fapi.withone.ai%2Fopen%2Fcount%2Fplatforms" alt="platforms"></a>
  &nbsp;
  <a href="https://withone.ai/knowledge"><img src="https://img.shields.io/endpoint?url=https%3A%2F%2Fapi.withone.ai%2Fopen%2Fcount%2Ftools" alt="tools"></a>
  &nbsp;
  <a href="./LICENSE"><img src="https://img.shields.io/badge/License-OKCL--1.0-blue.svg" alt="license"></a>
</p>

## Why

API documentation is scattered across hundreds of sites, buried in PDFs, locked behind developer portals, and constantly going stale. AI agents are left to guess at parameters, hallucinate auth flows, and fail silently on edge cases.

One Knowledge fixes this. We've built structured, human-verified knowledge for every tool across 500+ platforms and we're opening all of it. 80,000+ tools, every parameter, every auth flow, every edge case. Structured for machines. Verified by humans. Free forever.

[Browse it all →](https://withone.ai/knowledge)

## Quick Start

The fastest way to get knowledge into your agent is through the [One CLI](https://github.com/withoneai/cli):

```bash
npm install -g @withone/cli
one init
```

That's it. The CLI will prompt you for your API key (get one free from the [One Dashboard](https://app.withone.ai/settings/api-keys)) and configure everything for your environment: Claude Code, Cursor, Claude Desktop, Windsurf, or any MCP-compatible agent.

Once connected, your agent can search for actions, read full knowledge, and execute tools across all 500+ platforms.

## API

Access knowledge programmatically with the open API. All you need is a free [One API Key](https://app.withone.ai/settings/api-keys).

All requests require the `x-one-secret` header:

```
x-one-secret: YOUR_ONE_API_KEY
```

| Endpoint | Description |
|----------|-------------|
| `GET /open/knowledge/:platform` | Get a platform's overview |
| `GET /open/knowledge/:platform/auth` | Get a platform's authentication details |
| `GET /open/knowledge/:platform/actions` | List a platform's actions (paginate via `page` query param) |
| `GET /open/knowledge/:platform/actions/search?query=` | Search a platform's actions |
| `GET /open/knowledge/:platform/actions/:actionId` | Get an action's full knowledge |

**Base URL:** `https://api.withone.ai`

```bash
# Example: Get Airtable's knowledge
curl 'https://api.withone.ai/open/knowledge/airtable' \
  --header 'x-one-secret: YOUR_ONE_API_KEY'
```

For full API documentation, examples, and response schemas, see the [docs](https://withone.ai/docs).

## What's in the knowledge?

Every piece of knowledge is structured, complete, and ready for machine consumption:

| Component | Description |
|-----------|-------------|
| **Metadata** | Platform name, category, version, image, last updated date |
| **Authentication** | OAuth flows, required credentials, scopes, token refresh details |
| **Actions** | Every available API action with method, URL, headers |
| **Parameters** | Required and optional parameters with types and descriptions |
| **Enforcement Rules** | Constraints that ensure correct API usage (e.g., query params vs body) |
| **Response Schemas** | Full response structures with field types and descriptions |
| **Examples** | Real request/response examples for every action |

## Contributing

The knowledge is maintained by [One Systems Inc.](https://withone.ai) and verified by humans. If you find something outdated, incorrect, or missing, open an issue and we'll fix it.

- **[Report outdated or incorrect knowledge](../../issues/new?template=report-outdated-knowledge.yml)** - an action's parameters changed, auth flow updated, endpoint deprecated, etc.
- **[Request a new platform](../../issues/new?template=request-new-platform.yml)** - a platform you'd like to see added to the knowledge base.

## License

This project is licensed under the [One Knowledge License v1.0](./LICENSE).

The knowledge is free to use, modify, and distribute with attribution. See the full license for details on metadata integrity, AI training usage, and community contributions.
