# LocAPI agent skill

This repository is the public LocAPI skill. It tells an agent how to call the hosted MCP server and the REST API at `https://locapi.dev`.

The source of truth in the monorepo is `packages/skill`. Pushes to `main` publish this directory to [github.com/locapi-hq/skill](https://github.com/locapi-hq/skill). Create that empty repository once; the split workflow fills it.

## Install

Copy `SKILL.md` into the skills directory of the agent you use. Keep the file name `SKILL.md`.

### Cursor

```bash
mkdir -p .cursor/skills/locapi
curl -fsSL -o .cursor/skills/locapi/SKILL.md \
  https://raw.githubusercontent.com/locapi-hq/skill/main/SKILL.md
```

Restart Cursor so it loads the skill.

### Claude Code

```bash
mkdir -p .claude/skills/locapi
curl -fsSL -o .claude/skills/locapi/SKILL.md \
  https://raw.githubusercontent.com/locapi-hq/skill/main/SKILL.md
```

### Codex

```bash
mkdir -p .agents/skills/locapi
curl -fsSL -o .agents/skills/locapi/SKILL.md \
  https://raw.githubusercontent.com/locapi-hq/skill/main/SKILL.md
```

### Any other agent

Put `SKILL.md` in that agent's skills folder. Point the agent at the file if it does not load skills automatically. The agent still needs `LOCAPI_API_KEY` from the [LocAPI console](https://locapi.net/console/api-keys).

## What the skill does not do

It does not embed an API key and it does not run a local MCP process. The MCP server is already hosted at `https://locapi.dev/mcp/geo`.
