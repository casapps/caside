## Project description

Caside is an all-in-one integrated development environment that combines
traditional code editing with a built-in autonomous AI coding agent (CASAI),
business management tools, social media automation, billing systems, and a
complete release/signing pipeline. Every VS Code-class productivity feature
ships as a native, always-on, compiled-in capability — there is no plugin or
extension marketplace. Caside is intended as a full replacement for Vim/
Neovim, VS Code, Zed, and Antigravity as a developer's day-to-day editor —
not a similar-class alternative alongside them, but a single application
that removes the need to install or run any of them. The goal is to be the
single application a developer needs from initial idea through production
deployment and ongoing business operation: editor, git client, debugger,
terminal, API tester, database admin tool, PDF/document signer, release
manager, and back office (billing, support, social media) in one product.

## Project variables

project_name:     caside
project_org:      casapps
# FROZEN — set once at first-time setup, never edit
internal_name:    caside
# FROZEN — set once at first-time setup, never edit
internal_org:     casapps
app_name:         Caside
crate_name:       caside
official_site:
maintainer_name:  casjay
maintainer_email: git-admin@casjaysdev.pro

## Business logic

**Target users:**
- Individual developers who want editor + AI agent + release pipeline in one tool
- Indie/solo developers who also need business tooling (billing, support, social
  posting) without separate SaaS subscriptions
- Teams needing shared project configuration, git workflow, and release signing

**Surfaces (GUI/TUI/CLI only — no feature gating; all three expose the same
core capabilities, differing only where an interaction genuinely requires a
pointing device, e.g. drag-and-drop diagram layout):**
- GUI: yes — native desktop, Windows/macOS/Linux, both X11 and Wayland
- TUI: yes — full feature parity with GUI wherever terminal rendering allows
- CLI: yes — scriptable entry points for every capability (agent tasks, shell
  completion generation, release builds, git operations, business-tool CRUD)
- Web: out of scope — no browser-hosted frontend, no PWA. The "built-in web
  browser" and "API testing tool" features below are native GUI/TUI/CLI
  features, not a web app

---

### Built-in editor & code intelligence

- **Editor core**: efficient handling of very large files, incremental syntax
  highlighting, multi-cursor editing, full Vim-compatible modal editing
  (motions, text objects, operators, macros, registers, visual mode, Ex
  commands, marks/jumps, configurable leader key, surround-style add/change/
  delete of enclosing pairs), semantic code folding, snippet expansion,
  Emmet-style markup-abbreviation expansion (HTML/CSS/JSX), auto-closing
  brackets and quotes, delimiter-based text alignment/tabularization, bracket
  matching with rainbow colorization, indent guides, live inline error/
  warning highlighting with quick fixes, paired-tag auto-rename (HTML/XML/
  JSX), and inline color swatches for CSS/hex/RGB color values
- **New-file header templates**: optionally auto-inserts a configurable file
  header (author, contact, license, creation date, description) into newly
  created files, matching the project's own header convention
- **Native Language Server Protocol client**: built directly into the editor
  core (not a plugin) for completion, diagnostics, go-to-definition/
  references, rename, and hover documentation against any language's LSP
  server; the same client also drives Tailwind/utility-CSS-class completion,
  hover preview, and linting when such a config is detected in the project
- **Notebook support**: open, edit, and execute Jupyter-style notebooks
  (code and markdown cells, kernel selection, rendered cell output) inline
  in the editor, for data-science and exploratory-analysis workflows
- **Built-in language tool manager**: downloads, version-pins, updates, and
  isolates per-language LSP servers, debug adapters (DAP), linters, and
  formatters on request, so a language "just works" without the user
  manually installing its tooling first; managed installs live under Data
  (see Stored data location) and never touch the host's own package manager
- **Formatting & linting**: per-language auto-detected formatter and linter
  execution on save or on demand, with inline results (equivalent to
  Prettier/ESLint/rustfmt-clippy style tooling for every supported language),
  honoring a project's `.editorconfig` (indent style/size, line endings,
  charset, trailing-whitespace/final-newline rules) as the baseline ahead of
  any language-specific formatter config
- **Native built-in linters/validators**: for the most common formats — Bash/
  POSIX shell, fish, Dockerfiles, YAML, TOML, Markdown, HTML, PHP, Ruby,
  JSON, and JavaScript/TypeScript, with more added over time — validation and
  linting run compiled directly into the caside binary, with no external
  process invocation and nothing to fetch or install first; the Built-in
  language tool manager (above) remains the path for languages without a
  native validator yet, or when the user explicitly wants the canonical
  upstream formatter/linter instead of caside's built-in one
- **Inline diagnostics + project-wide diagnostics panel**: end-of-line and
  hover diagnostic messages from the language server and linters (Error
  Lens-equivalent), plus a dedicated panel aggregating every warning/error
  across the whole project, filterable by severity/file/source (Trouble-
  equivalent)
- **Comment annotations**: recognizes and visually distinguishes TODO/FIXME/
  HACK/NOTE/WARNING comment prefixes inline in the editor (Better Comments-
  equivalent) and surfaces the same scan results as the aggregated task list
  described under Project planning — one underlying scanner, two views
- **Unified fuzzy finder**: one fuzzy-search interface (invoked from a single
  keybinding/command) across files, project-wide symbols, open buffers/tabs,
  recent projects, git status/branches, and live text search across the
  project (Telescope-equivalent); filesystem-path autocomplete while typing
  string literals/imports is available inline as you type (Path
  Intellisense-equivalent)
- **Keybinding discoverability**: a popup showing available keybindings/
  commands for the current mode and any typed prefix, plus a searchable
  command palette (which-key-equivalent)
- **File explorer**: a persistent project tree sidebar (create/rename/move/
  delete, drag-and-drop, git-status decoration) alongside the fuzzy finder
- **Spell checking**: inline spell-check for comments, strings, and prose
  files (Markdown, plain text) with a project-level custom dictionary
- **Structured file intelligence**: schema-aware validation and completion
  for YAML, JSON, TOML, Dockerfiles, Compose files, and Kubernetes manifests,
  plus column-aligned highlighting for CSV/TSV files
- **Gremlins detection**: scans for invisible/zero-width/direction-control
  Unicode characters, mixed line endings, and Trojan Source-style attacks,
  with severity levels and inline warnings in a dedicated gutter lane
- **Markdown & diagram preview**: live-rendered Markdown preview including
  embedded diagram syntax, side-by-side or pop-out
- **Session & workspace persistence**: reopening a project restores the
  previous layout, open files, cursor positions, and terminal state; a start
  screen offers recent projects and quick actions (new/clone/open) on launch
- **Remote & containerized development**: attach to a remote host over SSH or
  to a running container/dev-container-style environment and edit as if
  local, including remote terminal and remote debugging
- **Theming & iconography**: built-in dark/light/auto theme engine with a
  bundled icon set mapped by file type/language; user-installable custom
  themes are data (color/style definitions), not executable code
- **Real-time collaborative editing**: peer-to-peer shared editing sessions
  (Live Share-equivalent) — a host shares a live session directly with
  invited peers (no hosted relay/session server), with shared cursors,
  shared terminal, and shared debug sessions; falls back to the normal git
  workflow (push/pull/PRs) for asynchronous collaboration when a live
  session isn't in use

### Git & hosting integration

- Full local workflow: init/clone, branch/switch/merge/rebase, worktrees,
  staged and line-level partial commits, push/pull with credential-helper
  and SSH-agent integration, stash, tag, submodules, hooks, LFS-tracked
  files, and optional commit signing (GPG/SSH) with a signed/unsigned status
  indicator per commit using the same certificate/key store described under
  Security
- Visual tooling: syntax-highlighted diff viewer, interactive line-level
  staging, commit graph with branch visualization, per-line blame integrated
  directly into the editor gutter, file history browser, interactive rebase
  and cherry-pick, visual merge-conflict resolution
- Hosting provider integration: GitHub, GitLab, Gitea, Bitbucket, and Azure
  DevOps — issues, pull/merge requests, CI pipeline status, releases
- Release tagging is managed from the same panel as day-to-day git operations
  (one Git panel, not a separate release-tag tool)

### Debugging & testing

- Multi-language debugger front end (breakpoints with conditions, variable
  inspection/modification, call stack view, watch expressions, REPL console)
  driving a debug adapter for the target language — either already installed
  on the host or fetched on request by the built-in language tool manager
  described under Built-in editor & code intelligence
- Test runner integration: discovery, execution, and result visualization for
  the project's test framework(s), inline pass/fail/coverage indicators in
  the gutter, benchmark execution and historical performance tracking, and
  flaky-test detection from repeated-run history (a test that alternates
  pass/fail across otherwise-identical runs is flagged, not silently retried
  and forgotten)

### Terminal

- Embedded terminal supporting multiple concurrent instances, scrollback
  search, and environment/process inspection
- Split panes within the terminal area, persistent sessions that survive an
  app restart (see Session & workspace persistence), and a configurable
  default shell/profile per platform (bash/zsh/fish/PowerShell/whatever the
  user has installed) with per-project shell overrides
- Editor-terminal integration: open a terminal pre-set to the active file's
  directory, and run the current file or the project's detected test/build
  command directly from the editor, its output landing in a terminal pane

### API testing tool

- HTTP, WebSocket, and GraphQL request builder with collections, environment
  variables, auth handling, scripted assertions, request chaining (using one
  request's response in the next), and a mock-server mode (this is caside's
  REST-client feature — there is no separate "REST Client" extension
  equivalent, it lives only here)
- One-time import of existing Postman/Insomnia collections for migration,
  after which collections live as caside's own project data (git-trackable,
  diffable), not as a synced dependency on the originating tool

### Database administration

- Query editor, schema browser, migration runner, and backup/restore for
  PostgreSQL, MySQL, SQLite, MongoDB, and Redis connections the user
  configures; connects to databases the user already runs, does not bundle
  or manage database servers itself
- Connection credentials are stored in the same encrypted vault as every
  other credential category, never in a project file; a read-only connection
  mode is available as a safety option for production databases
- Query results export to CSV/JSON; frequently-used queries save as named,
  reusable snippets per connection
- Schema browser can render an ER-diagram view of a database's tables and
  relationships using the same diagram engine described under Diagram tool
  (one diagram engine, populated from a database schema, hand-drawn shapes,
  or CASAI analysis — not three separate diagramming systems)

### Built-in web browser

- Tabbed browsing with standard navigation, bookmarks, and a lightweight
  inspector (view source, DOM/element inspection)
- Documentation-lookup shortcuts (language docs, MDN, Stack Overflow, the
  project's git host) and automatic error-message research
- Detects a locally running dev server and offers live-reload preview;
  pop-out into an independent window, including picture-in-picture, for a
  second monitor

### PDF editing & document signing

- In-place PDF text/image/form-field editing, page insert/delete/reorder,
  and annotation tools, operating on the PDF's native text layer. OCR/text
  recognition for scanned, image-only documents is out of scope entirely —
  not planned for any version
- Digital and electronic signature workflows: certificate-based signing,
  reusable document templates (contracts, NDAs), client signature requests,
  signature verification, and a tamper-evident audit trail
- Certificate lifecycle management for signing identities is shared with the
  Security section below — one certificate store, used by both PDF signing
  and release/code signing, not two separate implementations

### Business management

- Client management with contact and engagement history; support for
  running multiple distinct businesses/brands from one install, each with
  its own clients, invoice numbering, and financial reporting
- Invoicing and billing: customizable invoice templates, estimates/quotes
  that convert to an invoice on client acceptance, recurring/subscription
  invoices with configurable billing cycles, automated late-fee application
  and payment-reminder scheduling, payment processing through the user's own
  Stripe/PayPal/Square account, dunning management, multi-currency support,
  regional tax calculation
- A client-facing portal link (no client-side account/login required) where
  a client can view and pay an invoice or estimate; this is the only part of
  Business management a client ever sees directly
- Expense tracking and categorization, time tracking tied to client/project
  billing, financial reporting

### Social media automation

- Scheduled and templated posting to Twitter/X, LinkedIn, Facebook,
  Instagram, Mastodon, and Threads, triggerable manually or automatically
  from a release/milestone event
- Content queue/calendar with per-platform preview and cross-platform
  formatting (character limits, image sizing, hashtag conventions per
  platform)
- Engagement analytics: per-post reach, likes/reactions, comments, shares,
  and link clicks pulled from each platform's own API into one aggregated
  dashboard; organic posting and analytics only — no ad-buying or paid
  promotion management, that is out of scope

### Support system

- Ticketing with categorization and SLA tracking, a searchable knowledge
  base, canned/templated responses, and optional CASAI-assisted first-pass
  responses to common questions (routed through the same multi-provider AI
  backend described under CASAI — not a separate AI integration)
- Multi-channel ticket intake: created directly in-app, or generated from an
  inbound support email the user connects; every ticket links to the
  submitting client's record from Business management — one client entity
  shared across billing and support, not two separate contact lists
- SLA breach warnings surface on the Project planning dashboard alongside
  project tasks and milestones, not in a separate notification silo

### Project planning

- Tasks, milestones, and Gantt-style scheduling; budget tracking; progress
  dashboards
- An aggregated project task list sourced from TODO/FIXME/HACK/NOTE comment
  scanning (the same scanner used by the editor's comment annotations,
  above) merged with manually created planning tasks in one view
- Local-only coding-activity analytics (WakaTime-equivalent): automatic
  time-in-editor tracking per project/file/language shown on the progress
  dashboard, distinct from the manually-entered, client-billable time
  tracking described under Business management; never leaves the device
  unless the user explicitly configures an external analytics endpoint

### Diagram tool

- Drag-and-drop architecture/network/flow diagramming with a library of
  common shapes (servers, databases, users, network devices) and smart
  connector routing, exported as PNG/SVG
- CASAI can generate a first-draft diagram from analysis of the current
  project's code and dependency structure, which the user then edits by hand
  (one diagram engine, populated either manually or via CASAI — not two
  separate diagramming systems); the same engine also renders database
  ER-diagrams described under Database administration
- Diagrams are stored as project data files alongside the code they
  document, git-trackable and diffable like any other project file, not
  held in a separate diagram-tool data store

### Release management

- Cross-platform binary, container image, and package builds (RPM, DEB, MSI,
  PKG, AppImage, Snap, Flatpak, IPA, APK/AAB, and FreeBSD/OpenBSD/NetBSD
  native packages)
- Multi-platform code signing: macOS (Developer ID / notarization), Windows
  (Authenticode/EV), Linux (GPG package and repo signing), Android (keystore
  signing), iOS (provisioning-profile signing) — signing identities are
  managed in the same certificate store used by PDF/document signing
- SBOM generation, checksum generation, and signature/attestation generation
  for every release artifact
- Publishing to package registries (crates.io, npm, PyPI, etc.), app stores,
  container registries, git-host releases, Linux package repositories, and
  cloud deployment targets the user configures

### Security

- Dependency, container-image, and static-analysis vulnerability scanning;
  secret-detection scanning across code and commit history; license
  compliance checking against the allow/deny lists AI.md defines
- Scans run on demand or on a user-configured schedule; findings surface in
  the project-wide diagnostics panel described under Built-in editor & code
  intelligence, plus a dedicated Security findings view for triage, severity
  filtering, and marking a finding as accepted-risk/false-positive
- Certificate lifecycle management (issuance tracking, renewal reminders,
  revocation checking) shared by PDF signing and release signing
- Encryption at rest for the credential vault and in transit for all network
  calls the application makes
- Audit log of security-relevant events (vault access, signing operations,
  credential changes, panic-disable triggers), stored locally under Logs and
  never transmitted unless the user explicitly exports it

### Sync

- Optional sync of safe settings (never credentials) across user-configured
  cloud storage (Google Drive, Dropbox, OneDrive, iCloud Drive, Nextcloud/
  ownCloud, S3-compatible, Azure Blob, WebDAV)
- Optional git-backed team settings repository for sharing non-secret,
  project-level configuration across a team, with normal git-based conflict
  resolution

### No plugin ecosystem — everything above is built in

Every feature in this document compiles into the single `caside` binary and
is always available; there is no runtime plugin loading, no dynamic loading
of arbitrary code, and no extension marketplace. Themes and templates
(document templates, snippet libraries, diagram shapes) are user-editable
*data*, not executable code, and are not a plugin mechanism.

### CASAI — the built-in autonomous coding agent

**What CASAI is:** CASAI is caside's own task-orchestration layer, not a
thin wrapper around one AI vendor. It plans and executes multi-step
development tasks inside the current project by driving whichever AI
backend(s) the user has configured (see Multi-provider AI support, below).
CASAI is available from a dedicated sidebar panel, a command-palette
shortcut, and a CLI entry point (`caside agent "<request>"`, an interactive
chat mode, and a background-execution mode with status polling).

**How CASAI works, end to end:**
1. **Directory-aware context** — on opening a project or changing directory,
   CASAI loads that directory's own conversation history and memory (prior
   tasks, learned preferences, prior solutions), kept separate per project.
2. **Task intake** — the user describes a task in natural language, via
   chat, a CLI request, or a background task.
3. **Planning** — CASAI decomposes the request into an ordered list of
   concrete steps (files/commands touched) and classifies each step's risk:
   read-only, in-place edit, or destructive/privileged.
4. **Safety gate** — any destructive or privileged step (deleting files,
   force-pushing, a system-scope install, sending an invoice, posting to
   social media, signing a release) requires explicit user confirmation
   before it runs; CASAI never executes higher-risk actions silently.
5. **Execution with live feedback** — approved steps run one at a time with
   real-time progress reporting (status line, log, and optional voice
   announcements at a user-chosen verbosity level); a failed step is retried
   within a bounded budget and then reported explicitly — CASAI never stalls
   silently or claims success without having acted.
6. **Live control** — while a task runs, slash commands let the user pause,
   resume, stop, restart, adjust verbosity, or ask for an explanation of the
   current step, without losing task state.
7. **Memory & learning** — on completion, CASAI stores a summary of the task,
   the approach taken, and any corrections the user made, into that
   directory's memory for future recall; the vault's credentials are never
   written into this memory.
8. **Working-set discipline** — CASAI only reads and writes inside the
   current project root unless the user explicitly names a path outside it.
9. **Framework awareness** — when scaffolding a feature (auth flow, CI/CD
   pipeline, infrastructure files, a database migration) CASAI detects the
   target project's own language/framework and generates code that matches
   it; this applies to whatever project the user has open, which need not be
   a Rust project — CASAI is a tool for building other software, and caside
   itself remains Rust-only regardless of what CASAI is asked to generate.
10. **Offline fallback** — with no AI backend configured or reachable, CASAI
    still performs deterministic, template-driven versions of common tasks
    (project scaffolding, install-script generation, routine build-error
    fixes) without requiring a live AI call.

**Multi-provider AI support** (the backend CASAI calls, and the same backend
used for inline code completion and support-ticket first-pass responses —
one integration, three consumers):
- Supported out of the box: Anthropic Claude, GitHub Copilot, OpenAI Codex/
  GPT, local models via Ollama, and any OpenAI-compatible custom endpoint —
  this list is illustrative, not exhaustive; additional providers can be
  added as compiled-in modules
- Local/self-hosted backends (Ollama, a custom endpoint) connect directly
- Paid backends connect in whichever of two modes the user selects per
  provider: (a) the provider's API using a user-supplied key stored in the
  encrypted vault, or (b) the provider's own CLI/subscription tool, already
  installed and authenticated on the user's machine, invoked as a local
  subprocess
- All provider integrations are compiled-in Rust modules selected by
  configuration, not runtime plugins

**Built-in MCP server** (the reverse integration direction — external AI
tools driving caside, rather than caside consuming an AI provider):
- Caside exposes its own capabilities — file/project operations, git
  operations, editor and diagnostics state, CASAI task delegation, and
  read/write access to the business-tool data — as an MCP server, so any
  MCP-compatible AI client (Claude Code, Claude Desktop, or another agent)
  can drive caside directly instead of only being driven by it
- Local-only by default: the MCP server listens on a local transport
  (invoked as a subprocess or a local-only socket), with no network exposure
  unless the user explicitly opts in and configures authentication
- Every capability exposed over MCP goes through the same safety gate CASAI
  itself uses — a destructive or privileged action requested by an external
  MCP client still requires explicit user confirmation (or a pre-approved
  automation policy the user configured up front), it is never auto-approved
  just because the request came from an external tool instead of CASAI
- This makes caside usable two ways at once: as a full IDE with its own
  built-in agent (CASAI), and as a tool/backend another AI agent can operate

**Data models (high level — full schemas belong in an implementation doc, not
here):**
- Project: type, workspace root, per-project config overrides
- Credential vault entry: category (ai/social/git/signing/cloud/billing),
  encrypted payload, cache policy (session TTL, sensitivity tier)
- CASAI conversation: keyed by working-directory path hash; stores history,
  learned patterns, preferences, and task memory
- Client / Invoice / Ticket / Social post / Certificate: business-tool and
  signing-identity entities

**User flows:**
- Open a directory → project auto-detected → CASAI loads directory-scoped
  conversation/context → editor, gutter, and sidebar populate
- `caside agent "task"` → CASAI plans → confirms any risky steps → executes
  with visible real-time progress → reports the result or asks for input on
  genuine ambiguity
- Code → commit and push (git panel) → tag a release → the release pipeline
  builds, signs, and publishes to configured targets → optional social post
  announcing the release, either triggered manually or by CASAI on request

**Business rules:**
- Safe settings (editor/UI/preferences, provider selection — never
  credentials) and the encrypted credential vault (API keys, social/git/
  cloud tokens, signing certificates and private keys) are stored in
  physically separate locations so settings alone are always safe to
  version-control or sync; see Stored data location, below
- The application itself is never paywalled or license-gated; the billing
  feature exists to invoice the *user's own clients*, which is unrelated to
  caside's own distribution terms
- Credential cache lifetime is sensitivity-aware (e.g. signing certificates
  cache briefly, social tokens longer, billing credentials shortest) with a
  global panic-disable to clear all cached credentials immediately
- CASAI must never silently fail a promised task — the user always gets
  either visible progress or an explicit failure report

**Platform constraints:**
- Target OS: Windows 10+, macOS 10.15+, Linux, FreeBSD, NetBSD, OpenBSD;
  x86_64 and ARM64, statically linked with no host libc version dependency
  on Linux/BSD
- GUI runs on both X11 and Wayland on Linux; X11 on BSD targets

**Performance & size targets** (the payoff for "no plugin ecosystem, no
Electron, statically-linked Rust"):
- Release binary size target: under 300MB per platform, in line with other
  full-featured editors, despite shipping every feature in this document
  compiled in with no optional/plugin-loaded slimming
- Startup time and idle memory/CPU usage are expected to beat Electron-based
  competitors (VS Code, Antigravity) by a substantial margin, since there is
  no embedded browser runtime, no extension host process, and no plugin
  marketplace machinery to load — this is a direct consequence of the
  single-binary, no-plugin, compiled-Rust architecture, not a separate
  workstream
- Where a feature's native implementation would meaningfully blow past the
  size target (e.g. a bundled rendering engine), the constraint is resolved
  by trimming that feature's implementation approach, not by cutting the
  feature from this document — size/performance tradeoffs are an
  implementation-doc concern, scope stays as defined here

**Outbound network use:**
- Configured AI provider APIs and local model endpoints; paid-provider CLI/
  subscription tools invoked as local subprocesses make their own outbound
  calls independently of caside
- Git hosting provider APIs (GitHub/GitLab/Gitea/Bitbucket/Azure DevOps)
- Social media platform APIs
- Payment processor APIs (Stripe/PayPal/Square)
- Cloud storage/sync provider APIs
- Package registry / app store / container registry publishing APIs
- User-configured external database connections (Database administration)
- Documentation lookup via the built-in browser

**Stored data location (per-user, following AI.md's path rule):**
- Config (safe settings only): `~/.config/casapps/caside/`
- Data (encrypted vault, CASAI conversations/memory, business-tool data):
  `~/.local/share/casapps/caside/`
- Cache: `~/.cache/casapps/caside/`
- Logs: `~/.local/state/casapps/caside/logs/`
- Optional team-shared project config: `.caside/` inside a project (data
  only — editor/UI preferences and workflow templates, never credentials)

**License exceptions:**
- Local relational storage for structured business-tool data (clients,
  invoices, tickets) uses a vendored-C SQL engine under a permissive
  (public-domain/MIT-equivalent) license, which requires an exception to
  AI.md's Rust-Only Application rule (vendored-C, not a build-time host
  toolchain dependency); no denylisted license is involved, so no
  `distribution_license` project variable is needed
- No other exceptions: no runtime plugin/extension loading, no `dlopen`, no
  WASM plugin host — AI.md's plugin-system prohibition applies as-is since
  caside has no plugin ecosystem
- No SvelteKit/Node.js or other non-Rust toolchain contributes to the binary

**Scope resolution (reconciled with user 2026-07-18):**
- Every feature listed above ships inside the single `caside` binary, per
  AI.md's single-binary rule — no companion apps, no Cargo feature-gating of
  any of the above; everything listed is always compiled in and always
  available on GUI, TUI, and CLI alike
- The web surface is out of scope to satisfy the Rust-only constraint; the
  "no plugin ecosystem" decision replaces what would otherwise have been a
  WASM plugin host with built-in equivalents of the most common VS Code
  extensions, enumerated by category above
