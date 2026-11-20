# Agent-Ready Audit

Check whether a website is ready for AI agents. Give it a URL and a list of tasks (find a product and reach
checkout, sign up, log in, compare offers); it runs a **static scan** (robots.txt and AI-bot rules, llms.txt,
sitemap, schema.org, semantic HTML/ARIA, form labels, bot walls, public API/MCP/NLWeb) and a **swarm of AI
browser agents** that act like a personal assistant, then shows an **Agent-Readiness Score (0–100)** and a
report of what the agents could and couldn't do, with fixes, in a web dashboard.

**Status:** planning. The full plan and architecture (in Polish) are in [`docs/PLAN.md`](docs/PLAN.md).

## Stack (planned)

- Python 3.12, [uv](https://docs.astral.sh/uv/)
- Dashboard: FastAPI + Jinja2 + HTMX
- Agents: Claude Code sessions via [claude-agent-sdk](https://pypi.org/project/claude-agent-sdk/) on a personal Claude subscription (no API key), driving a local Chromium through the [browser-use](https://github.com/browser-use/browser-use) `==1.0.6` MCP server (Playwright MCP as fallback)
- Static scanner: httpx + Playwright
- Storage: SQLite (later Postgres), local artifact store for screenshots

## Configuration

Copy `.env.example` to `.env` and fill it in. Never commit `.env` — this repository is public.
The subscription mode is for personal use on your own machine only (Anthropic's terms); an optional `api` backend
with an API key exists for anything else.

## Responsible use

Only audit sites you own or have written permission to test. Agents stop before any real payment and use
test accounts only. See the security section of the plan.
