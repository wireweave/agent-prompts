# @wireweave/agent-prompts

Canonical grammar prompts for LLM agents that generate Wireweave DSL. The package is the single source of truth so consumers (`agent-harness`, `api-server`, future plugins) stay in sync with the multi-page canvas model in `@wireweave/core` 3.x.

## Install

```bash
pnpm add @wireweave/agent-prompts
```

## Use

```ts
import { buildGrammarPrompt, buildCompactGrammarPrompt } from '@wireweave/agent-prompts'

// Full prompt — generation phase.
const system = buildGrammarPrompt()

// Compact prompt — analyze / plan phases (saves ~800 tokens).
const compact = buildCompactGrammarPrompt()
```

Both functions return a single Markdown-flavoured string that can be injected verbatim into an LLM system message. No runtime dependencies.

## What's covered

- Single-page wireframes (legacy).
- **Multi-page canvas** — multiple top-level `page` declarations, `at(x, y)` positioning, `viewport="WxH"`.
- Renderer surface from `@wireweave/core`: `render(doc)` / `renderCanvas(doc)` / `renderPage(page)`.
- Layout / content / form / nav / data / feedback / overlay / utility component contracts.
- Mapping common UI concepts to DSL components.

## Why a separate package

Before this package the DSL grammar guide was duplicated in
`api-server/src/services/guide.ts`, `api-server/src/agent/prompts.ts`, and
`agent-harness/wireweave/src/guide.ts`. The agent-harness copy drifted to a
pre-3.0 single-page-only definition, which silently broke multi-screen
wireframe generation. Pulling the guide into its own package gives a single
versioned export every downstream consumer can pin.

## License

MIT
