# Creators Butler — Self‑Sufficiency Skill Checklist

Use this checklist as acceptance criteria for the Sealed Manager Kernel (SMK), Toolsmith, Evaluator, Deployer, and the initial Specialists.

## A) Kernel governance & policy
- [ ] Kernel image is **read‑only**; updates require dual signatures (verified at boot).
- [ ] `policy.yaml` loaded and **enforced** (budgets, allowlists, red lines, dual‑control).
- [ ] Denials return **machine‑readable reason codes**; all checks logged to audit.
- [ ] **Kill switch** halts actions instantly; read‑only status/audit remain live.

## B) Toolsmith (auto‑developer)
- [ ] Generates a new **Specialist** from a directive (scaffold + tests + container).
- [ ] Registers Specialist in **Registry of Tools** with I/O **JSON Schemas**, SLOs, and cost profile.
- [ ] Pins deps; emits **SBOM**; passes license allowlist (MIT/Apache/BSD).
- [ ] Submits a **Change Proposal** (spec, risk, tests, rollback plan).

## C) Evaluator (quality & safety)
- [ ] Runs **unit/integration/E2E** tests and **red‑team** prompts.
- [ ] Performs **SAST** (bandit/semgrep), **image scan** (no High/Critical).
- [ ] Benchmarks **latency/cost** vs budget; enforces RAG ≤ 10s SLO.
- [ ] Rejects on failures; writes a complete eval report to audit.

## D) Deployer (progressive + rollback)
- [ ] Canary rollout (5%→50%→100%) with **automatic rollback** on SLO breach.
- [ ] Content‑addressed artifacts; **versioned** configs; one‑click revert.
- [ ] Health checks + metrics exposed; rollout events captured in audit.

## E) Knowledge & memory (RAG)
- [ ] Watches docs folder and **embeds with provenance**.
- [ ] Answers include **source‑linked citations**; abstains when evidence is weak.
- [ ] Supports **PII tagging/retention**; exports **redact** by default.

## F) Household specialists (minimum viable)
- [ ] **Archivist (RAG)** built by Toolsmith at runtime; passes RAG QA.
- [ ] **Concierge** drafts emails, proposes calendar events, composes **daily brief**.
- [ ] **GroceryPlanner**: vendor allowlist + weekly spend cap; suggests only (Phase 1).
- [ ] **Ops/Guardian**: enforces budgets/allowlists/dual‑control on all tickets.

## G) Autonomy loop (safe self‑improvement)
- [ ] **Sense → Plan → Act → Evaluate → Learn → Gate → Deploy/Rollback** loop implemented.
- [ ] Proposes **small prompt/tool diffs**; promotes only on eval win; logs diffs with provenance.
- [ ] Schedules **weekly red‑team** and dependency scans; files issues or auto‑fixes.

## H) Hardware adaptation (self‑tuning)
- [ ] Detects GPU VRAM/RAM/disk throughput & driver versions at boot.
- [ ] Chooses backend (vLLM/llama.cpp/etc.), **quantization** and batch sizes.
- [ ] Benchmarks vs baseline; **promotes** only if faster/cheaper; otherwise **rolls back**.
- [ ] Prepares human‑run scripts for OS/driver upgrades (no privileged self‑patching).

## I) Safety, security, compliance
- [ ] **Least‑privilege** secrets; rotation; no plaintext `.env` in Git.
- [ ] **Network allowlist** enforced (registries/model hubs only); no scraping.
- [ ] **Role/age awareness** (adults/minors/guest); door/alarms always dual‑control.
- [ ] Immutable **audit log** of intents, inputs, tool I/O, costs, and policy decisions.

## J) Efficiency & footprint (scored)
- [ ] Working‑set **RAM+VRAM** within targeted tier (≤12/16/24/32 GB).
- [ ] **On‑disk** footprint minimized (pulled images + `/models`).
- [ ] **Cold‑start** to all `/healthz` ≤ 90s.
- [ ] Meets RAG **≤10s** SLO; else no efficiency credit.

## K) Reliability & ops
- [ ] **Backups**: nightly snapshot of `/data` (+ tested restore).
- [ ] **Observability**: metrics (latency, error, cost), logs, status page.
- [ ] **Idempotent** retries; timeouts; circuit‑breakers for flaky deps.
- [ ] **Incident runbook** auto‑generated; postmortems recorded in wiki.

## L) Human interface & UX
- [ ] **Daily brief**: schedule, tasks, incidents, proposed upgrades, spend vs caps.
- [ ] Clear **escalation prompts** when action exceeds policy (with reason + options).
- [ ] Tone/style consistent with “Butler” persona; refusals are helpful and specific.

## M) Ventures (self‑sufficiency path)
- [ ] **Data‑Cleaning Microservice** (audited transforms; CSV in/out; pricing config).
- [ ] or **Research Briefs** (citations, confidence notes; unit cost per report).
- [ ] Basic **billing hooks** (draft invoices/logs; no payments needed for bounty).
- [ ] KPI surfaces: unit cost, gross margin, turnaround time, quality score.

## N) Trading‑sim (optional, paper‑only)
- [ ] Paper broker mock; risk caps; **Promotion Gates** (OOS + paper pass).
- [ ] Immutable trade logs and **refusal rules**; no live keys or ToS violations.

---

## Milestones (how we’ll grade progress)
- **M0 Draft‑only:** Policy + audit + RAG citations; no live actions; kill works.
- **M1 Low‑risk autonomy:** GroceryPlanner/Concierge plan under caps; Toolsmith builds Archivist; Evaluator/Deployer gate changes.
- **M2 Self‑upgrade:** hardware detection → backend switch via canary; rollback verified; weekly red‑team and backups pass.
- **M3 Revenue‑ready:** one Ventures specialist operating end‑to‑end (draft invoices/logs) with unit‑economics dashboard.

## Evidence expected at acceptance
- **Artifacts:** RoT entries (JSON), Change Proposals, eval reports, deployment logs.
- **APIs:** `/v1/daily_brief`, `/v1/audit/stream`, `/v1/control/kill` visible in `make demo`.
- **Harness:** policy/RAG/autoupgrade/kill/restore tests pass; efficiency metrics printed.
