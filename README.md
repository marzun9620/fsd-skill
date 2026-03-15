# FSD Architect - Claude Code Skill

> Feature-Sliced Design architecture guardian for React, Next.js, Remix, and React Router projects.

[![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-green)](https://claude.com/claude-code)

## What it does

**FSD Architect** enforces [Feature-Sliced Design](https://feature-sliced.design) methodology in your frontend codebase. It activates automatically when you create or modify frontend files and ensures:

- **Layer hierarchy** - App → Pages → Widgets → Features → Entities → Shared
- **Import direction** - Modules only import from layers strictly below
- **Public API enforcement** - Every slice exports through `index.ts`
- **Segment conventions** - `ui/`, `model/`, `api/`, `lib/`, `config/`
- **Framework integration** - Thin route wrappers for React Router 7, Next.js App Router, Remix
- **Naming conventions** - kebab-case directories, PascalCase components, explicit named exports

## Installation

### As a Claude Code plugin

```bash
claude plugin add github:marzun9620/fsd-skill
```

### Manual installation (project-level)

```bash
mkdir -p .claude/skills/fsd-architect
curl -o .claude/skills/fsd-architect/SKILL.md \
  https://raw.githubusercontent.com/marzun9620/fsd-skill/master/skills/fsd-architect/SKILL.md
```

### Manual installation (global)

```bash
mkdir -p ~/.claude/skills/fsd-architect
curl -o ~/.claude/skills/fsd-architect/SKILL.md \
  https://raw.githubusercontent.com/marzun9620/fsd-skill/master/skills/fsd-architect/SKILL.md
```

## Usage

### Automatic

The skill activates automatically when you ask Claude to create components, restructure code, or work on frontend files. Claude will validate against FSD rules.

### Manual

```
/fsd-architect UserProfileCard
```

Pass a component or slice name as an argument to get FSD-compliant scaffolding.

## Example

Ask Claude:

```
Create a new "notifications" feature with a NotificationList component and a useNotifications hook
```

Claude will create:

```
src/features/notifications/
├── index.ts              # Public API
├── ui/
│   └── NotificationList.tsx
└── model/
    └── useNotifications.ts
```

With proper imports only from `@/entities/` and `@/shared/`, and a clean `index.ts`:

```ts
export { NotificationList } from "./ui/NotificationList";
export { useNotifications } from "./model/useNotifications";
```

## Compatibility

| Framework              | Support                    |
| ---------------------- | -------------------------- |
| React + React Router 7 | Full (thin route wrappers) |
| Next.js App Router     | Full (page re-exports)     |
| Next.js Pages Router   | Full (page re-exports)     |
| Remix                  | Full (thin route wrappers) |
| Vite + React           | Full                       |
| Astro                  | Partial (pages layer)      |

## FSD Layers at a Glance

```
App        → Routing, providers, global styles (no slices)
Pages      → Full screens, route compositions
Widgets    → Large reusable UI blocks
Features   → User interactions (forms, actions)
Entities   → Business concepts (user, product, order)
Shared     → UI kit, API client, utils, i18n (no slices)
```

**The Golden Rule:** Import only **downward**. Never up, never sideways.

## Contributing

PRs welcome! If you use FSD with a framework not covered, please open an issue or PR.

## License

MIT
