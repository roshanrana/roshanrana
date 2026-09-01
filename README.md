# Roshan Rana

FinTech integrations and delivery specialist with 18 years of experience, focused on the practical edge where customer workflows, production systems, AI, and audit expectations meet.

I build portfolio projects around the kinds of constraints that matter in financial services: messy client data, deterministic fallbacks, explainable AI boundaries, human review, event contracts, local reproducibility, and evidence that a reviewer can verify without trusting a slide deck.

## Featured Work

| Project | What it shows | Technologies | Validation evidence |
| --- | --- | --- | --- |
| [MarketSage](https://github.com/roshanrana/MarketSage) | MCP-native market intelligence workbench that connects LLM clients to a traditional analyst workflow: Go MCP gateway, OpenBB-ready market data boundary, Hugging Face finance dataset manifest, sentiment/evidence pipelines, saved research runs, source caveats, and a polished web workbench. | Go, MCP, Python, FastAPI, DuckDB, OpenBB-ready adapter, Hugging Face datasets/models, TypeScript MCP SDK, Next.js, React, GitHub Actions. | `npm run check`, 15 Python tests, Go fmt/test/vet, MCP CLI smoke across 7 tools plus saved-run resource, Next.js production build, desktop/mobile browser verification, `npm audit`, `uv pip check`, `govulncheck`. |
| [LedgerLens](https://github.com/roshanrana/LedgerLens) | AI-assisted financial reconciliation with deterministic-first matching, bounded LLM adjudication, human review, audit-ready reports, and a Go/Kafka sidecar path. | Python, SQLite, Go, Docker, Kafka/Redpanda-compatible events, JSON schemas, CLI/API workflows. | Python unit/contract/golden/e2e tests, CLI smoke, Dockerized Go worker tests, worker image build, Python-to-Go event replay, compose validation, optional Redpanda round trip. |
| [RegLens](https://github.com/roshanrana/RegLens) | Regulatory intelligence/RAG system for compliance teams with grounded citations, quote verification, durable chat sessions, source lifecycle audit, and fail-closed provider controls. | FastAPI, Python, SQLite, BM25, hybrid retrieval, optional Qdrant, optional OpenAI providers, optional cross-encoder reranking, Docker. | Deterministic fake-mode verifier, lint, strict typing, offline tests, eval harness, audit-chain verification, optional browser/Qdrant/OpenAI/model/container profiles, GitHub Actions. |
| [PROVENANCE](https://github.com/roshanrana/PROVENANCE) | LLM infrastructure governance for regulated environments: reproducible inference attestations and tenant-isolated prefix-cache routing for shared vLLM/llm-d platforms. | Python, uv, pytest, NumPy/SciPy, cryptography, Go, vLLM, llm-d, Kubernetes/kind, Helm-style manifests. | `make check`, 200+ tests, coverage gates, `make attest-demo`, signed receipt tamper tests, statistical decision tests, Go salt-derivation tests, documented GPU/cluster hardware gates. |

## Portfolio Theme

These projects are intentionally FinTech-leaning and enterprise-delivery shaped:

- They start from operational problems a financial institution would recognize: market research, reconciliation, regulatory intelligence, and controlled AI infrastructure.
- They keep AI bounded by workflow, evidence, costs, and human or audit review.
- They include local demos and deterministic test paths so an interviewer can clone and verify the work quickly.
- They expose integration surfaces: MCP tools/resources, CLIs, APIs, event contracts, Docker profiles, audit exports, and runbooks.
- They document tradeoffs clearly, including what has been validated and what still requires hardware or live provider credentials.

## What I Optimize For

- Customer-specific onboarding without brittle one-off code.
- Reliability before cleverness: deterministic defaults, fake providers, typed boundaries, and repeatable verification.
- Auditability: source provenance, hash chains, signed receipts, evidence digests, and reviewer-readable reports.
- Practical AI systems: use rules and retrieval where they are stronger; call models only behind explicit contracts.
- Delivery discipline: build the slice, prove the slice, and leave the next engineer with a runbook.

## Links

- [LinkedIn](https://www.linkedin.com/in/roshanrana/)
- [GitHub](https://github.com/roshanrana)
