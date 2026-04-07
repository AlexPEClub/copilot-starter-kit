# AI Coding Starter Kit

> Build production-ready web apps faster with AI-powered Prompts handling Requirements, Architecture, Development, QA, and Deployment.

This template uses [GitHub Copilot](https://docs.github.com/en/copilot) with Prompts, Instructions, and Custom Agents to provide a complete AI-powered development workflow.

## Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/YOUR_USERNAME/ai-coding-starter-kit.git my-project
cd my-project
npm install
npx playwright install chromium   # one-time: installs browser for E2E tests (~300MB)
```

### 2. (Optional) Supabase Setup

If you need a backend:

1. Create Supabase Project: [supabase.com](https://supabase.com)
2. Copy `.env.local.example` to `.env.local`
3. Add your Supabase credentials
4. Uncomment the Supabase client in `src/lib/supabase.ts`

Skip this step if you're building frontend-only (landing pages, portfolios, etc.)

### 3. Start Development

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 4. Initialize Your Project

Open Copilot Chat and describe your project. The `/requirements` prompt automatically detects that this is a fresh project and enters **Init Mode**:

```
/requirements I want to build a project management tool for small teams
where users can create projects, assign tasks, and track progress.
```

The prompt will:
1. Ask interactive questions to clarify your vision, target users, and MVP scope
2. Create your **Product Requirements Document** (`docs/PRD.md`)
3. Break the project into individual features (Single Responsibility)
4. Create all **feature specs** (`features/PROJ-1.md`, `PROJ-2.md`, etc.)
5. Update **feature tracking** (`features/INDEX.md`)
6. Recommend which feature to build first

You don't need to put everything in the first prompt - a brief description is enough. The prompt asks follow-up questions interactively.

### 5. Build Features

After project initialization, build features one at a time using prompts:

```
/architecture    Design the tech approach for features/PROJ-1-user-auth.md
/frontend        Build the UI for features/PROJ-1-user-auth.md
/backend         Build the API for features/PROJ-1-user-auth.md
/qa              Test features/PROJ-1-user-auth.md
/deploy          Deploy to Vercel
```

Each prompt suggests the next step when it finishes. Handoffs are always user-initiated.

To add more features later, run `/requirements` again - it detects the existing PRD and adds a single feature.

---

## Available Prompts

| Prompt | Command | What It Does |
|--------|---------|-------------|
| Requirements Engineer | `/requirements` | Creates feature specs with user stories, acceptance criteria, edge cases |
| Solution Architect | `/architecture` | Designs PM-friendly tech architecture (no code, only high-level design) |
| Frontend Developer | `/frontend` | Builds UI with React, Tailwind CSS, and shadcn/ui |
| Backend Developer | `/backend` | Builds APIs, database schemas, RLS policies with Supabase |
| QA Engineer | `/qa` | Tests features against acceptance criteria + security audit |
| DevOps | `/deploy` | Deploys to Vercel with production-ready checks |
| Help | `/help` | Context-aware guide: shows where you are and what to do next |

### How It Works

- **Prompts** are defined in `.github/prompts/` and auto-discovered by Copilot (type `/` in chat)
- **Instructions** in `.github/instructions/` are auto-applied based on file context (via `applyTo` globs)
- **Custom Agents** in `.github/agents/` run as specialized subagents for frontend, backend, and QA
- **copilot-instructions.md** in `.github/` provides project context automatically at every session start

---

## Development Workflow

```
1. Define    /requirements  -->  Feature spec in features/PROJ-X.md
2. Design    /architecture  -->  Tech design added to feature spec
3. Build     /frontend      -->  UI components implemented
             /backend       -->  APIs + database (if needed)
4. Test      /qa            -->  Test results added to feature spec
5. Ship      /deploy        -->  Deployed to Vercel
```

### Feature Tracking

Features are tracked in `features/INDEX.md`:

| ID | Feature | Status | Spec |
|----|---------|--------|------|
| PROJ-1 | User Login | Deployed | [Spec](features/PROJ-1-user-login.md) |
| PROJ-2 | Dashboard | In Progress | [Spec](features/PROJ-2-dashboard.md) |

Every skill reads this file at start and updates it when done, preventing duplicate work.

---

## Tech Stack

| Category | Tool | Why? |
|----------|------|------|
| **Framework** | Next.js 16 | React + Server Components + App Router |
| **Language** | TypeScript | Type safety |
| **Styling** | Tailwind CSS | Utility-first CSS |
| **UI Library** | shadcn/ui | Copy-paste, customizable components |
| **Backend** | Supabase (optional) | PostgreSQL + Auth + Storage + Realtime |
| **Deployment** | Vercel | Zero-config Next.js hosting |
| **Validation** | Zod | Runtime type validation |

---

## Project Structure

```
ai-coding-starter-kit/
+-- .github/
|   +-- copilot-instructions.md      <-- Auto-loaded project context
|   +-- instructions/                <-- Auto-applied coding rules (via applyTo)
|   |   +-- general.instructions.md      Git workflow, feature tracking
|   |   +-- frontend.instructions.md     shadcn/ui, component standards
|   |   +-- backend.instructions.md      RLS, validation, queries
|   |   +-- security.instructions.md     Secrets, headers, auth
|   +-- prompts/                     <-- Invocable workflows (/command)
|   |   +-- requirements.prompt.md       /requirements
|   |   +-- architecture.prompt.md       /architecture
|   |   +-- frontend.prompt.md           /frontend
|   |   +-- backend.prompt.md            /backend
|   |   +-- qa.prompt.md                 /qa
|   |   +-- deploy.prompt.md             /deploy
|   |   +-- help.prompt.md              /help
|   |   +-- assets/                  <-- Templates & checklists
|   |       +-- feature-template.md      Feature spec template
|   |       +-- qa-test-template.md      QA results template
|   |       +-- frontend-checklist.md    Frontend completion checklist
|   |       +-- backend-checklist.md     Backend completion checklist
|   +-- agents/                      <-- Custom agent configs
|       +-- frontend-dev.agent.md        Frontend specialist
|       +-- backend-dev.agent.md         Backend specialist
|       +-- qa-engineer.agent.md         QA specialist
+-- features/                        <-- Feature specifications
|   +-- INDEX.md                         Status tracking
|   +-- README.md                        Spec format documentation
+-- docs/
|   +-- PRD.md                       <-- Product Requirements Document
|   +-- production/                  <-- Production setup guides
|       +-- error-tracking.md            Sentry setup (5 min)
|       +-- security-headers.md          XSS/Clickjacking protection
|       +-- performance.md               Lighthouse, optimization
|       +-- database-optimization.md     Indexing, N+1, caching
|       +-- rate-limiting.md             Upstash Redis
+-- src/
|   +-- app/                         <-- Pages (Next.js App Router)
|   +-- components/
|   |   +-- ui/                      <-- shadcn/ui components (35+ installed)
|   +-- hooks/                       <-- Custom React hooks
|   +-- lib/                         <-- Utilities
+-- public/                          <-- Static files
```

---

## Getting Started

### 1. Fill Out Your PRD

Define your product vision in `docs/PRD.md`:
- What are you building and why?
- Who are the target users?
- What features are on the roadmap?

### 2. Build Your First Feature

Run `/requirements` with your feature idea. The prompt will:
- Ask interactive questions to clarify requirements
- Create a feature spec in `features/PROJ-1-name.md`
- Update `features/INDEX.md` with the new feature
- Suggest running `/architecture` as the next step

### 3. Add shadcn/ui Components (as needed)

35+ components are pre-installed. Add more as needed:
```bash
npx shadcn@latest add [component-name]
```

### 4. Production Setup (first deployment)

When you're ready to deploy, the `/deploy` prompt guides you through:
- Vercel setup and deployment
- Error tracking with Sentry
- Security headers configuration
- Performance monitoring with Lighthouse

See `docs/production/` for detailed setup guides.

---

## How It Works Under the Hood

### Prompts (`.github/prompts/`)
Each prompt is a structured workflow that Copilot discovers automatically when you type `/` in chat. Prompts define the step-by-step process for each role (Requirements Engineer, Architect, Developer, QA, DevOps).

| Prompt | What It Does |
|--------|-------------|
| `/requirements` | Interactive feature specification with user stories and acceptance criteria |
| `/architecture` | PM-friendly tech design (no code, visual component trees) |
| `/frontend` | Build UI with shadcn/ui, Tailwind, responsive design |
| `/backend` | APIs, database schemas, RLS policies, Zod validation |
| `/qa` | Systematic testing, E2E tests, security audit |
| `/deploy` | Vercel deployment with production-ready checks |
| `/help` | Quick status check and next-step guidance |

### Instructions (`.github/instructions/`)
Coding standards that are auto-applied based on which files Copilot is working with (via `applyTo` globs). No manual loading needed.

### Custom Agents (`.github/agents/`)
Specialized agents for frontend, backend, and QA work with restricted tool sets for focused, efficient execution.

### copilot-instructions.md
Auto-loaded at every session start. Contains tech stack, conventions, and references to PRD and feature index.

---

## Context Engineering

AI agents work best with clean, structured context - not longer prompts. This template is designed around these principles:

### State lives in files, not in memory

Every prompt reads `features/INDEX.md` and the relevant feature spec at start. After a new session, nothing is lost - the agent simply re-reads the files. Progress tracking, acceptance criteria, and tech designs all live in markdown files, not in the conversation.

### Context is layered

Not everything is loaded at once. Information is layered by relevance:

| Layer | What | When loaded |
|-------|------|-------------|
| `copilot-instructions.md` | Tech stack, conventions, commands | Every session (auto) |
| `.github/instructions/` | Coding standards | When editing matching files (auto via `applyTo`) |
| Prompt `.prompt.md` | Workflow instructions | When prompt is invoked (via `/command`) |
| Feature spec | Requirements, AC, tech design | On demand (prompt reads it) |
| `docs/production/` | Deployment guides | Only when referenced |

### Context recovery is built in

All prompts include a **Context Recovery** section: if context is lost mid-task, the agent re-reads the feature spec, checks `git diff` for progress, and continues without restarting or duplicating work.

### Always read, never guess

A global instruction (`instructions/general.instructions.md`) enforces: always read a file before modifying it, never assume contents from memory, verify import paths and API routes by reading. This prevents hallucinated code references - the most common source of AI coding errors.

---

## Customization for Your Team

This template is designed as a starting point. Customize it for your team:

1. **Edit `.github/copilot-instructions.md`** - Add your project-specific conventions and build commands
2. **Edit `docs/PRD.md`** - Define your product vision and roadmap
3. **Edit `.github/instructions/`** - Adjust coding standards for your team
4. **Edit `.github/prompts/`** - Modify workflows to match your process
5. **Edit `.github/agents/`** - Configure agent specializations

---

## Production Guides

Standalone guides in `docs/production/`:

| Guide | Setup Time | What It Does |
|-------|-----------|-------------|
| [Error Tracking](docs/production/error-tracking.md) | 5 min | Sentry integration for automatic error capture |
| [Security Headers](docs/production/security-headers.md) | 2 min | XSS, Clickjacking, MIME sniffing protection |
| [Performance](docs/production/performance.md) | 10 min | Lighthouse checks, image optimization, caching |
| [Database Optimization](docs/production/database-optimization.md) | 15 min | Indexing, N+1 prevention, query optimization |
| [Rate Limiting](docs/production/rate-limiting.md) | 10 min | Upstash Redis for API abuse prevention |

---

## Scripts

```bash
npm run dev          # Development server (localhost:3000)
npm run build        # Production build
npm run start        # Production server
npm run lint         # ESLint
npm test             # Vitest: integration tests for API routes
npm run test:e2e     # Playwright: E2E tests for user flows
npm run test:all     # Run both test suites
```

---

## Author

Created by **Alex Sprogis** – AI Product Engineer & Content Creator.

- [YouTube](https://www.youtube.com/@alex.sprogis)
- [Website](https://alexsprogis.de)

---

## License

MIT License - feel free to use for your projects!
