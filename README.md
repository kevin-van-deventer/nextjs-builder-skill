# Next.js Builder Agent Skill Installer

This package provides a comprehensive, high-fidelity agent skill installer for Next.js 15+, React 19, and advanced Technical SEO playbooks. It is designed to be installed locally within an agent workspace or globally for agentic workflows (e.g. Claude Code, Antigravity, Codex).

## Target Architectures

- **Framework**: Next.js 15+ (App Router) & React 19 (Server Actions + `useActionState`).
- **Styling**: Tailwind CSS with slugified custom business-name prefixes.
- **Performance**: Partial Prerendering (PPR), suspense boundary routing, and Google Fonts self-hosting.
- **SEO & GEO**: E-E-A-T narrative verification, BLUF AI-engine formatting, speakable schemas, and unified connected graph JSON-LD.
- **Hosting**: Edge performance, s-maxage CDNs, WWW redirects (Vercel edge, Netlify redirects).

---

## Installation & Execution

### 1. Run via Local Node Script
To install the skill in your current active agentic workspace:
```bash
node ./nextjs-builder-skill/bin/install.mjs antigravity
```

### 2. Run globally (npx)
Once published or linked:
```bash
npx nextjs-builder-skill antigravity
```

### Available Targets
- `claude-code`          → `~/.claude/skills/nextjs-builder`
- `codex`                → `~/.codex/skills/nextjs-builder`
- `antigravity`          → `.agents/skills/nextjs-builder` (workspace-local)
- `antigravity-global`   → `~/.gemini/antigravity/skills/nextjs-builder`
- `all`                  → Install to all directories
