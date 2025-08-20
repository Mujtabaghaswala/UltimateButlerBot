[![Releases](https://img.shields.io/badge/Releases-Download-blue?style=for-the-badge&logo=github)](https://github.com/Mujtabaghaswala/UltimateButlerBot/releases)

# UltimateButlerBot — Self-Upgrading Local AI Agent for DevOps

![butler-robot](https://images.unsplash.com/photo-1603791440384-56cd371ee9a7?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=8ef5ef6c7d8a6cf5da4e0f3d9b3c2f5c)

Short description
- UltimateButlerBot runs on a sealed kernel as a local agent that writes, tests, and deploys tools for you.
- It self-upgrades and aims for minimal footprint, safe defaults, and strong ops hygiene.
- This repo is part of a bounty: sealed-kernel local agent that auto-codes & deploys tools. Self-upgrading. Scored for safety, ops, and footprint. 10k payout.

Badges
- ![AI Safety](https://img.shields.io/badge/ai--safety-verified-green)
- ![LLM](https://img.shields.io/badge/llm-local--llm-orange)
- ![Docker](https://img.shields.io/badge/docker-supported-blue)
- Topics: ai-safety, artificial-intelligence, autonomous-agents, bounty, competition, devops, docker, docker-compose, fastapi, generative-ai, large-language-models, llm, local-llm, machine-learning, mlops, pgvector, rag, retrieval-augmented-generation, self-hosted, vector-database

Table of contents
- Features
- Quickstart (download & run)
- Architecture
- Components
- Safety and scoring
- Self-upgrade mechanism
- Deployment options
- CLI and API
- Tests and metrics
- Contributing
- License
- Releases

Features ⚙️
- Local-first agent that runs inside a sealed kernel container.
- Auto-code pipeline that writes, lints, tests, and deploys microservices.
- Self-upgrading agent with strict audit logs.
- Scored for safety, operational readiness, and footprint.
- Vector search using pgvector and RAG for tool specs.
- Support for local LLMs and remote model adapters.
- Docker and docker-compose templates for easy setup.
- FastAPI control plane and a compact CLI agent.

Quickstart — Download & Run ▶️
- Download the latest release artifact. The file in Releases must be downloaded and executed.
- Releases: https://github.com/Mujtabaghaswala/UltimateButlerBot/releases

Steps (Linux/macOS)
1. Download the release archive from the Releases page above.
2. Extract: tar -xzf ultimate-butlerbot-<version>.tar.gz
3. Enter folder: cd ultimate-butlerbot-<version>
4. Run the installer: ./install.sh
5. Start the agent: ./run-agent.sh

Windows
1. Download the release ZIP from the Releases page above.
2. Extract and run setup.bat as admin.
3. Start the agent via run-agent.bat.

System requirements
- 4 CPU cores (8 recommended)
- 8 GB RAM (16 GB recommended for local LLM use)
- 20 GB disk for base install; add more for vector DB and model stores
- Docker 20.10+ and docker-compose 1.29+ for container workflows
- Optional: GPU + CUDA if you run local LLMs that use GPU

Architecture diagram
![architecture](https://raw.githubusercontent.com/omnidan/node-emoji/master/lib/emoji.json)

High-level flow
- Control Plane (FastAPI): receives tasks and user prompts.
- Agent Core: plans, writes code, runs unit tests, and deploys.
- RAG Layer: stores tool specs and docs in pgvector. Uses retrieval to ground agent plans.
- Local LLM Adapter: wraps local models or remote ones via adapter.
- Ops Runner: container orchestration via Docker Compose or k8s manifests.
- Audit Log: append-only audit trail stored in sealed storage.

Components explained
- FastAPI Control Plane
  - Exposes a REST API to submit tasks.
  - Provides health endpoints and metrics.
- Agent Core
  - Planner: breaks tasks into steps.
  - Code Generator: emits project files and CI configs.
  - Tester: runs unit and integration tests in ephemeral sandboxes.
  - Deployer: builds images and deploys via docker-compose or k8s manifests.
- RAG and Vector DB
  - pgvector stores semantic embeddings of docs and tools.
  - Retriever fetches relevant context for the LLM.
- LLM Adapter
  - Supports local-llm backends (Llama, MPT) and remote endpoints.
  - Includes a safety filter and context window manager.
- Sealed Kernel Container
  - Runs the agent with minimal host privileges.
  - Uses seccomp, user namespaces, and read-only mounts.
- Self-upgrade Controller
  - Verifies signature of new code.
  - Runs upgrades in a staging sandbox before switching.

Safety and scoring 🛡️
- Safety policy
  - Principle: fail-safe defaults. The agent refuses destructive ops without explicit human approval.
  - Action gates: any write to production requires a signed approval token.
  - Capability bounding: network and filesystem access restrict by default.
- Scoring model
  - Safety score: evaluates action gating, sandboxing, and audit coverage.
  - Ops score: evaluates reproducible deploys, rollback strategy, and runtime health checks.
  - Footprint score: measures memory, disk, and CPU use on default tasks.
- Tests included
  - Safety tests simulate common risky prompts.
  - Ops tests verify deploy and rollback paths.
  - Footprint tests run a fixed workload and report peak usage.

Self-upgrade mechanism 🔁
- Signed releases
  - Each release carries a GPG signature and a SHA256 manifest.
- Staged rollout
  - The agent downloads the release artifact to a staging dir.
  - It runs a complete test suite in a sandbox container.
  - If tests pass and signatures validate, the agent swaps symlinks to activate the new version.
- Rollback
  - The agent keeps the last two working versions.
  - Rollback runs in under 30 seconds in common cases.
- Audit trail
  - Every upgrade step writes to the append-only audit log with user, version, timestamp, and checksums.

Deployment options 🚀
- Docker Compose (recommended for local testing)
  - docker-compose.yml includes FastAPI, pgvector, agent, and optional model server.
  - Compose brings up a small cluster for dev.
- Kubernetes (advanced)
  - Helm chart included for production.
  - Uses PodSecurityPolicy constraints and network policies.
- Single-host sealed kernel
  - Run the agent inside a sealed kernel container for the highest isolation.

Example workflows
- Auto-code a utility
  - POST /tasks with a task spec and test cases.
  - Agent sketches a plan, writes code, runs tests, builds an image, and posts the deployment URL.
  - Human approves production deploy if required by policy.
- Reproduce a bug
  - Provide logs and a runbook.
  - Agent retrieves relevant files from RAG and crafts a repro script.
- Create an ops script
  - Agent writes a Terraform, k8s manifest, or docker-compose snippet per the request.

CLI and API
- CLI
  - ubagent init — create a local project
  - ubagent run — run a task
  - ubagent status — view agent state and scores
  - ubagent upgrade — trigger a manual upgrade
- API
  - POST /api/v1/tasks — submit a task
  - GET /api/v1/tasks/{id}/status — check status
  - GET /api/v1/metrics — Prometheus metrics
  - API uses token-based auth. Use HTTPS in production.

RAG, embeddings, and vector DB
- Embeddings
  - Use open-source embedder or remote service.
  - Store vectors in pgvector in a normalized form.
- Indexing
  - Agent auto-indexes new tool specs and docs during install and upgrades.
- Retrieval
  - Use a k-NN search to find context for the LLM.
  - Retrieve up to N chunks based on similarity and recency.

Local LLM support
- Plug-in adapter for popular local models.
- Manage context windows and chunking for long docs.
- Use quantized models when needed to reduce footprint.
- Offload heavy inference to remote model endpoints when allowed.

Monitoring and metrics 📊
- Prometheus metrics available at /metrics.
- Precomputed safety and ops scores update after each task.
- Grafana dashboard templates included in /deploy/grafana.

Testing and CI
- Unit tests for core modules.
- Integration tests spin up a compose stack and run a sample task.
- Security tests check for privilege escalations and broken sandboxes.
- CI pipeline uses GitHub Actions with required checks:
  - lint, unit, integration, safety-smoke tests.

Developer notes
- Repo structure
  - /agent — core logic
  - /api — FastAPI service
  - /deploy — docker-compose, helm charts
  - /docs — design docs and safety policy
  - /tests — unit and integration tests
- Coding style
  - Use type hints.
  - Keep modules small and testable.
  - Write clear unit tests for edge cases.

Contributing 🤝
- We accept PRs that include tests and a short design note.
- To propose a change:
  - Fork the repo.
  - Create a feature branch.
  - Add tests and docs.
  - Open a PR with the security impact and footprint estimate.
- Review process
  - Each PR receives a security review and an ops review.
  - Critical changes require two maintainers to approve.

License
- MIT License in LICENSE file.

Releases
- Download and execute the file from the Releases page. The file in Releases must be downloaded and executed.
- Releases: https://github.com/Mujtabaghaswala/UltimateButlerBot/releases

Contact and support
- Open issues on GitHub for bugs and feature requests.
- Use discussions for design topics and bounty coordination.

Images and assets used
- Hero image from Unsplash (free license).
- Badges via img.shields.io.

Appendix: example task payload (JSON)
{
  "task_name": "create-health-check-service",
  "description": "Implement a small HTTP health check service with /health and unit tests",
  "runtime": "python:3.11",
  "tests": [
    {
      "name": "health-route",
      "command": "pytest tests/test_health.py"
    }
  ],
  "deploy": {
    "method": "docker-compose",
    "service_name": "health-check"
  },
  "approval_required": true
}

End of file