# AI Specifications & Development Rules

This repository contains a comprehensive set of development rules, standards, and AI agent configurations designed to work seamlessly with multiple AI coding copilots. The setup is portable and can be imported into any project to provide consistent, high-quality AI-assisted development.

It's highly recommended to be used along with Spec-Driven Development frameworks like [OpenSpec](https://github.com/Fission-AI/OpenSpec)

## 📁 Repository Structure

```
.
├── docs/                        # Development standards and specifications
│   ├── base-standards.md        # Core development rules (single source of truth)
│   ├── backend-standards.md
│   ├── frontend-standards.md
│   ├── documentation-standards.md
│   ├── api-spec.yml             # OpenAPI specification
│   ├── data-model.md            # Database and domain models
│   ├── development_guide.md
│   └── plans/                   # Fallback plan location (when OpenSpec is not installed)
├── ai-specs/
│   ├── agents/                  # Agent role definitions (backend, frontend, analyst, etc.)
│   └── skills/                  # Reusable skill prompts/workflows
│
├── AGENTS.md                    # Generic agent configuration
├── CLAUDE.md                    # Claude-specific configuration
├── codex.md                     # GitHub Copilot/Codex configuration
└── GEMINI.md                    # Gemini-specific configuration
```

## 🤖 Multi-Copilot Support

This repository uses **symbolic links** or **naming conventions** to support multiple AI coding copilots without duplication:

- **`AGENTS.md`** → Generic agent rules (works with most copilots)
- **`CLAUDE.md`** → Optimized for Claude/Cursor
- **`codex.md`** → Optimized for GitHub Copilot/Codex
- **`GEMINI.md`** → Optimized for Google Gemini

All these files reference the same core rules in `docs/base-standards.md`, ensuring consistency across different AI tools while allowing copilot-specific customizations.

### Why This Approach?

✅ **Single Source of Truth**: Core rules maintained in one place (`base-standards.md`)  
✅ **Copilot Compatibility**: Each AI tool finds its configuration using its preferred naming convention  
✅ **Zero Configuration**: Import into a new project and it works immediately  
✅ **Easy Updates**: Update rules once, all copilots benefit  
✅ **Portable**: Copy this structure to any project  

## 🚀 Quick Start

### Quick Start (1 Minute Setup)

Want to get started right away? Open your coding agent in your project and say:

```text
Please read and follow the instructions in this file to set up LIDR's spec-driven development workflow in my project: https://raw.githubusercontent.com/LIDR-academy/ai-specs/main/setup-sdd.md
```

Your coding agent will automatically install OpenSpec (if needed), initialize it, import this repository's standards/skills, and update your OpenSpec config context. Skip to Post-Installation when done.

Works with Claude Code, Cursor, Codex, Gemini, or any agent that can read and execute repository setup instructions.

### Post-Installation

After automated setup completes:

1. Customize `docs/` for your real stack, domain, and architecture
2. Ask coding agent to start a new worktree with a given name, in order to isolate developments. It will internally use the skill "using-git-worktrees"
2. Run the extended OpenSpec flow: `/enrich-us` → `/new` → `/ff` → `/apply` → `/verify` → `/archive` → `/commit`
3. Ask coding agent to clean the worktree when finished

### 1. (Recommended) Install and Initialize OpenSpec

OpenSpec works great with this repository and is recommended for a spec-driven workflow.

Quick Start requirements from OpenSpec official docs:

- Node.js `20.19.0` or higher

Install OpenSpec globally:

```bash
npm install -g @fission-ai/openspec@latest
```

Then navigate to your project and initialize:

```bash
cd your-project
openspec init
```

### 2. Import Into Your Project

Copy this repository into your project first, so the `docs/` and `ai-specs/` paths already exist when you configure OpenSpec:

```bash
# Clone or copy this repository into your project (`-n`: do not overwrite existing files so you keep project's original README)
cp -rn LIDR-ai-specs/* your-project/
```

### 3. Customize `docs/` for Your Project (Mandatory)

This step is required. If you skip it, your AI assistant will use generic technical context instead of your real project context.

Update the files in `docs/` to match your stack, architecture patterns, domain language, API contracts, and data model.

For detailed guidance and ready-to-use prompt examples, see [Customization](#-customization).

### 4. Point `config.yml` to Your `docs` Folder

After `openspec init` and after copying this repository, update your project's `config.yml` to include your technical context from `docs`.

Prompt example to automate this with your copilot:

```text
Update my openspec config.yml context to reference this repository's docs and ai-specs structure.

Requirements:
- Use docs/base-standards.md as the single source of truth.
- Include docs/backend-standards.md, docs/frontend-standards.md, docs/documentation-standards.md.
- Include docs/api-spec.yml and docs/data-model.md.
- Tell the agent to adopt ai-specs/agents/backend-developer.md for backend work and ai-specs/agents/frontend-developer.md for frontend work.
- Mention ai-specs/skills as workflow guidance.
- Keep all paths relative to the project root.
```

Example (`config.yml`):

```yml
context: |
  Tech stack: TypeScript, Node.js, Express, Prisma, Domain-Driven Design (DDD)
  Architecture: Clean Architecture with Domain, Application, and Presentation layers
  We use conventional commits
  Domain: LTI (Leadership. Technology. Impact) ATS platform
  All code, comments, documentation, and technical artifacts must be in English

  Project specs (single source of truth): All artifact creation and implementation MUST follow the project's technical context in ai-specs/. Read and apply these when creating or implementing:
  - docs/base-standards.md — core principles, TDD, language standards, links to backend/frontend/docs standards
  - docs/backend-standards.md — API, database, testing, security (backend changes)
  - docs/frontend-standards.md — React, UI/UX (frontend changes)
  - docs/api-spec.yml — API contracts and endpoint definitions
  - docs/data-model.md — domain and data model
  - docs/documentation-standards.md — docs structure and maintenance
  For implementation: adopt the relevant agent from ai-specs/agents/ (e.g. backend-developer.md for backend, frontend-developer.md for frontend). Use ai-specs/skills/ for workflow guidance when applicable.

# Per-artifact rules (optional)
# Add custom rules for specific artifacts.
rules:
  # Global: apply ai-specs when creating any artifact
  _global:
    - Before creating any artifact, read and apply docs/base-standards.md
    - For backend-related artifacts, read docs/backend-standards.md and adopt guidelines from ai-specs/agents/backend-developer.md
    - For frontend-related artifacts, read docs/frontend-standards.md and adopt guidelines from ai-specs/agents/frontend-developer.md
    - Use docs/api-spec.yml and docs/data-model.md for API and data consistency in specs and tasks
```

### 5. Verify Configuration

Your AI copilot will automatically load:
- **Claude/Cursor**: `CLAUDE.md` → `docs/base-standards.md`
- **GitHub Copilot**: `codex.md` → `docs/base-standards.md`
- **Gemini**: `GEMINI.md` → `docs/base-standards.md`

All paths and rules are configured to work seamlessly without manual adjustments.

## 💡 Usage: Official OpenSpec Workflow

The recommended workflow in this repository uses official OpenSpec commands:

1. **`/enrich-us`** (optional): refine a vague user story or idea
2. **`/ff`**: create all required OpenSpec artifacts
3. **`/apply`**: implement tasks one by one
4. **`/verify`**: validate implementation against the change artifacts
5. **`/archive`**: archive the completed change
6. **`/commit`**: create focused commit(s) after verification

Workflow reference image:

![OpenSpec custom workflow reference](https://drive.google.com/uc?export=view&id=1H5pAfjzpvYLlaGxJOrd6zox2Q87HxGkh)

### Example: End-to-End Flow

Use these commands in sequence:

```bash
/enrich-us SCRUM-10
/ff SCRUM-10
/apply SCRUM-10
/verify SCRUM-10
/archive SCRUM-10
/commit
```

Artifacts are managed through OpenSpec change directories during this flow.

### Useful Skills

Skills live in `ai-specs/skills/` and are mirrored into `.claude/skills/` and `.cursor/skills/` via relative symlinks, so any copilot can discover them. The agent loads a skill automatically when a request matches its description (per `AGENTS.md` §4). The most useful ones in day-to-day work are **`enrich-us`**, **`using-git-worktrees`**, **`writing-skills`**, and **`code-auditing`**:

- **`enrich-us`** — Analyze and enhance a vague Jira user story (or raw idea) into an implementation-ready ticket with acceptance criteria, technical detail, and edge cases. Use **before** planning to make sure the team and the AI agree on scope.
- **`using-git-worktrees`** — Set up an isolated workspace before starting feature work or executing a plan, with safe creation, baseline checks, copying of local Claude settings, and a complete cleanup workflow when the work is done.
- **`writing-skills`** — Author and verify new skills (or refactor existing ones) following TDD-style validation before deployment. Use when adding a skill to `ai-specs/skills/` or editing an existing `SKILL.md`.
- **`code-auditing`** — Run a systematic 6-phase code quality audit covering security, performance, type safety, dead code, and library best practices, ending with a prioritized action plan. Use for pre-release reviews, technical-debt sweeps, and dependency audits.

Other active skills in this repository: `commit`, `explain`, `meta-prompt`, `update-docs`. See each `ai-specs/skills/<name>/SKILL.md` for the full instructions.

#### Deprecated skills (kept for backward compatibility)

The following skills are **deprecated** and superseded by the official OpenSpec workflow described above. They remain in the repository so existing projects keep working, but new work should use the OpenSpec commands instead:

| Deprecated skill | Use instead |
|---|---|
| `plan-backend-ticket` | `/ff <ticket-id>` (creates the OpenSpec change with tasks) |
| `plan-frontend-ticket` | `/ff <ticket-id>` (creates the OpenSpec change with tasks) |
| `develop-backend` | `/apply <ticket-id>` (implements tasks one by one) |
| `develop-frontend` | `/apply <ticket-id>` (implements tasks one by one) |

The OpenSpec flow (`/enrich-us` → `/ff` → `/apply` → `/verify` → `/archive` → `/commit`) keeps planning, implementation, validation, and archival in a single spec-driven artifact tree, instead of relying on standalone planning/implementation prompts. Prefer it for any new feature.

## 📖 Core Development Rules

All development follows principles defined in `docs/base-standards.md`:

### Key Principles

1. **Small Tasks, One at a Time**: Baby steps, never skip ahead
2. **Test-Driven Development (TDD)**: Write failing tests first
3. **Type Safety**: Fully typed code (TypeScript)
4. **Clear Naming**: Descriptive variables and functions
5. **English Only**: All code, comments, documentation, and messages in English
6. **90%+ Test Coverage**: Comprehensive testing across all layers
7. **Incremental Changes**: Focused, reviewable modifications

### Specific Standards

- **Backend Standards**: `docs/backend-standards.md`
  - API development patterns
  - Database best practices
  - Security guidelines
  - Testing requirements

- **Frontend Standards**: `docs/frontend-standards.md`
  - React component patterns
  - UI/UX guidelines
  - State management
  - Component testing

- **Documentation Standards**: `docs/documentation-standards.md`
  - Technical documentation structure
  - API documentation (OpenAPI)
  - Code documentation
  - Maintenance guidelines

## 🎯 Benefits

### For Developers
- ✅ **Consistent Code Quality**: AI follows the same standards every time
- ✅ **Comprehensive Testing**: Automatic 90%+ coverage across all layers
- ✅ **Complete Documentation**: API specs updated automatically
- ✅ **Faster Onboarding**: New team members reference the same rules
- ✅ **Reduced Review Time**: Code follows established patterns

### For Teams
- ✅ **Copilot Flexibility**: Team members can use their preferred AI tool
- ✅ **Knowledge Preservation**: Standards documented, not in people's heads
- ✅ **Quality Consistency**: Same standards regardless of who (or what) writes code
- ✅ **Easier Code Reviews**: Clear expectations and patterns
- ✅ **Scalable Practices**: Standards scale with the team

### For Projects
- ✅ **Maintainable Codebase**: Clean architecture and clear separation of concerns
- ✅ **Production-Ready Code**: TDD, error handling, and validation built-in
- ✅ **Living Documentation**: API specs and data models always current
- ✅ **Faster Feature Development**: Autonomous AI implementation from plans
- ✅ **Lower Technical Debt**: Best practices enforced from day one

## 🔧 Customization

### Adapting to Your Project

1. **Update technical context**: Find the different files in `docs` and modify core principles, coding standards, business rules and technical documentation to match your needs:
   - backend/frontend/testing/documentation standards
   - installation guide
   - data model
   - API docs
   - ...
2. **Adapt agents in `ai-specs/agents`**: Adjust agent definitions to your project's roles and workflows
3. **Extend skills in `ai-specs/skills`**: Define battle-tested prompts and workflows in reusable skills
4. **Link Resources**: Reference your project's specific documentation or tasks using MCPs
5. **Keep the symlink structure**: Remember to create relative symlinks from `.claude` and `.cursor` to the corresponding `ai-specs/agents` and `ai-specs/skills` entries to keep it consistent

### Prompt Example: Adapt Technical Context

Use this prompt with your copilot to adapt the `docs/` folder while preserving the same baseline structure:

```text
Following the same base structure already present in docs/, update all technical context documents according to this project's specifics.

Requirements:
- Keep the same document set and file names in docs/.
- Replace generic content with this project's real stack, architecture patterns, coding conventions, and domain terminology.
- Update backend, frontend, and documentation standards to reflect actual practices used by this team.
- Update docs/api-spec.yml and docs/data-model.md so they match the real endpoints and entities of this project.
- Ensure all references are internally consistent and aligned across docs/.
- Keep everything in English and make guidance implementation-ready for AI agents.
```

### Maintaining Standards

- **Single Source of Truth**: Always update `base-standards.md` first
- **Version Control**: Track changes to standards like code
- **Team Review**: Standards changes should be reviewed like pull requests
- **Documentation**: Keep examples current with actual implementation
- **Symlink Integrity**: After file renames/moves/suffix changes, verify and update all impacted symlinks
- **Canonical Placement**: Prefer `ai-specs` as canonical source and expose through symlinks for `.claude`/`.cursor` compatibility

## 📚 Technical context

### Reference Examples (from LIDR Project)

The following files are included as **reference examples** from the LIDR project. You should create your own versions tailored to your specific project:

- **API Specification**: `docs/api-spec.yml` (OpenAPI 3.0 format)
  - *Create your own API spec documenting your project's endpoints*
- **Data Models**: `docs/data-model.md` (Database schemas, domain models)
  - *Document your database structure and domain entities*
- **Development Guide**: `docs/development_guide.md` (Setup, workflows)
  - *Write setup instructions specific to your tech stack*


## 🤝 Contributing

When contributing to the standards:

1. Update `base-standards.md` (single source of truth)
2. Test with multiple AI copilots to ensure compatibility
3. Update generated examples in `changes/` (or `docs/plans/` fallback) if needed
4. Document breaking changes clearly
5. Follow the same standards you're defining!

## 📄 License

Copyright (c) 2025 LIDR.co
Licensed under the MIT License

**English:**

The content of this repository is part of the AI4Devs program by LIDR.co. If you want to learn to code with AI like the pros and get more templates and resources like these, you can find all the information on the official website: https://lidr.co/ia-devs

**Español:**

El contenido de este repositorio es parte del programa AI4Devs de LIDR.co. Si quieres aprender a programar con IA como los pros, y obtener más plantillas y recursos como estos, puedes encontrar toda la información en la página oficial: https://lidr.co/ia-devs

---

## 🙏 Acknowledgements

Some workflows and skill patterns in this repository are inspired by the Superpowers framework, especially around:

- `brainstorming`
- `using-git-worktrees`
- `writing-plans`
- `subagent-driven-development`
- `test-driven-development`

Superpowers project: [obra/superpowers](https://github.com/obra/superpowers/tree/main)

Additional inspiration/source acknowledgements:

- `code-auditing` skill: inspired by and adapted from [jeffrigby/somepulp-agents](https://github.com/jeffrigby/somepulp-agents/tree/main)

**Made with 🤖 by the LIDR community**

For questions, issues, or suggestions, visit [LIDR.co](https://lidr.co/ia-devs)

