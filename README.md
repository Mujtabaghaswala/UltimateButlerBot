# Creators Butler Bounty (Starter Repo)

This repository contains the **public bounty brief** and a **Starter Kit** scaffold for teams.

## QuickStart
```bash
# Run from repo root
cd starter-kit
make up          # bring up skeleton services
make demo        # run the demo script (stub)
make down        # stop everything
```


> **Timeline:** Launch Aug 11, 2025 → Submissions due **January 01, 2026** (23:59 CT)

## Structure
- `docs/` – Full bounty brief, judging procedure, and anti-gaming notes.
- `starter-kit/` – Compose file, sample policy, mocks, seeds, and a basic harness outline.
- `.github/` – Templates for issues/PRs.

## Submission Checklist (copy into your PR/ZIP)
- [ ] Repo link + commit hash
- [ ] `compose.yml`, `README.md`, `Architecture.md`, `Runbook.md`
- [ ] `policy.yaml`, `policy.schema.json`
- [ ] Demo script (`make demo`) and logs
- [ ] SBOMs & scan reports
- [ ] 3–5 min demo video

> **Note:** The Starter Kit includes **stub services** with `/healthz` endpoints so `make up` works out of the box. Replace stubs with your Sealed Manager Kernel (SMK), Toolsmith, Evaluator, Deployer, and Specialists.
