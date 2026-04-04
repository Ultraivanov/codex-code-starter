# Codex Code Starter

Single-agent meta-framework for structured AI-assisted development with **Codex**.

> Repository name remains `codex-code-starter` for long-term compatibility.

[![GitHub](https://img.shields.io/badge/GitHub-codex--code--starter-blue)](https://github.com/Ultraivanov/codex-code-starter)
[![Version](https://img.shields.io/badge/version-1.0.0-orange.svg)](https://github.com/Ultraivanov/codex-code-starter)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

> **RU version:** [README_RU.md](README_RU.md)

## Quick Links

- Start here: `init-project.sh`
- Codex entry point: `AGENTS.md`
- Changelog: `CHANGELOG.md`

## What Is New In v1.0.0

- Codex-first workflow contract with shared state files.
- Minimal, additive installation that never touches business code.
- Start/finish protocols aligned with Codex session boundaries.
- Simple project profiling for software vs content workstreams.

## Core Principles

- One shared project state for every Codex session.
- Deterministic start and finish routines.
- Zero impact on host business code.
- Clear separation between software and content projects.

## For Users

### Requirements

- Node.js 18+
- Python 3.x

Check:

```bash
node --version
python3 --version
```

### Installation Into Any Host Project

1. Download `init-project.sh` to the root of your host project.
2. Run installer:

```bash
./init-project.sh
```

Installer asks for **project profile**:

- `software` — for application/service/source-code projects.
- `content` — for course/book/article/research/script projects.

Each profile gets its own memory layout and generation logic.

3. Launch Codex in that project.
4. Start protocol in chat:

- `start`

5. Finish protocol in chat:

- `/fi`

## User Workflow

### Start

`start` runs cold start protocol:

- migration/upgrade routing (first run only),
- crash/session checks,
- shared context load,
- framework version check (auto-update path when available).

Context files are resolved by profile:

- software: `.codex/SNAPSHOT.md`, `.codex/BACKLOG.md`, `.codex/ARCHITECTURE.md`
- content: `.codex/content/SNAPSHOT.md`, `.codex/content/BACKLOG.md`, `.codex/content/ARCHITECTURE.md`

### Phase Workflow

This framework supports phase-based delivery. Rules live in:

- `.codex/protocols/phase-workflow.md`
- `.codex/PHASES.md` (current phase state)

On every `start`, Codex should load `PHASES.md`, confirm the active block, and proceed with a single block per session.

### Finish

`/fi` runs completion protocol:

- security/export checks,
- git status/diff checks,
- session finalization output.

## Framework Structure

```text
codex-code-starter/
├── AGENTS.md                     # Codex adapter entry
├── init-project.sh               # Installer for host projects
├── CHANGELOG.md
├── README.md
├── README_RU.md
├── LICENSE
├── .codex/
│   ├── commands/                 # Executable Codex workflows
│   │   └── quick-update.sh        # Codex updater entry
│   ├── protocols/                # Silent protocol specs
│   ├── templates/                # State/config templates
│   └── contracts/
├── security/                     # Security scan and cleanup scripts
└── migration/                    # Distribution/release tooling
```

## Migration Modes

Installer auto-detects host project type:

- `new` — clean project bootstrap,
- `legacy` — framework migration into existing project,
- `upgrade` — upgrade from previous framework generation.

In every mode, installer also sets project profile (`software` or `content`) in `.codex/.framework-config`.

All modes are designed to be non-destructive to host business code.

## Update Model

- `start` includes version check.
- If newer framework version is found and updater exists, update is applied automatically.
- Update payload is Codex-only to keep the runtime lean.

## FAQ

**Does it modify my code?**

No. The framework only adds `.codex/` state and helper scripts.

**Can I remove it later?**

Yes. Remove `.codex/` and `init-project.sh` to fully uninstall.

**How do phases work?**

Use `init-phases` to draft `.codex/PHASES.md`. Each session should run a single block, confirmed at `start`.

## For Framework Developers

### Setup

```bash
git clone https://github.com/Ultraivanov/codex-code-starter.git
cd codex-code-starter
```

### Build Distribution

```bash
bash migration/build-distribution.sh
```

Artifacts are created in `dist-release/`:

- `init-project.sh`
- `framework.tar.gz`
- `framework-commands.tar.gz`

## Versioning

- Semantic Versioning is used.
- `1.0.0` is the first stable release of the Codex-first contract.

See full details in [CHANGELOG.md](CHANGELOG.md).

## Contributing

1. Create branch
2. Make changes
3. Run local checks/build
4. Open PR

---

Framework goal: keep Codex sessions deterministic and portable while preserving a single, shared project state.
