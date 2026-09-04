# Roshan Rana

I take vendor platforms live inside large financial institutions. Eighteen years of it: collateral, payments, reconciliation, and now AI systems, always on the client's side of the change-control gate, always against a regulator's calendar rather than a project plan.

This is where I build in public. Every project here starts from an operational problem a bank would recognise, keeps AI bounded by evidence and human review, and ships with a deterministic path a reviewer can clone and verify in minutes. None of them are products. All of them are built to production constraints.

## Projects

Six systems. Each has an `OVERVIEW.md` (what it is and why) and a `SHOWCASE.md` (a guided tour of the features, with the commands to run) under `docs/`.

| | The problem | What it proves |
|---|---|---|
| **[SHADOWBOOK](https://github.com/roshanrana/shadowbook)** · Go, Python, PostgreSQL, Redpanda | Core-ledger migrations fail on the undocumented behaviour of the incumbent, not on the happy path. | A double-entry shadow ledger run alongside a legacy simulator carrying twelve seeded quirks, reconciled at three grains, with time-to-discovery measured per quirk. Delivery semantics measured against three real brokers killed mid-run: at-most-once both lost *and* duplicated. 243 tests; findings generated from artefacts, never hand-written. |
| **[HARBORMASTER](https://github.com/roshanrana/Harbormaster)** · Go, Python, Protobuf, Kafka, Postgres | Client, custodian and exchange files arrive under many names and formats; the reconciliation engine has to be told which client, which value date, and which of four price columns is the price. | Six event-driven services, a three-tier mapping ladder whose model dependence *decreases* as confirmed mappings promote into configuration, quarantine and four-eyes review, hash-chained audit, and twelve adversarial fixtures each with a named test. 379 tests; 100% attribution and value-date accuracy on the reference corpus. |
| **[PROVENANCE](https://github.com/roshanrana/PROVENANCE)** · Python, Go, vLLM, llm-d, Kubernetes | A bank runs one shared LLM inference platform across an information barrier. Batched inference is not reproducible, and the cache-aware router leaks which prefixes other tenants have used. | Signed inference receipts that anchor model identity to a Hugging Face commit and weight digest, connected to SR 11-7 validation; a cross-tenant KV-cache side channel found by reading llm-d source, closed with an out-of-tree scheduler plugin; pre-registered statistics, implemented rather than imported. 250 tests, 93% coverage. |
| **[LEDGERLENS](https://github.com/roshanrana/LedgerLens)** · Python, Go, SQLite, Kafka | Reconciliation teams want fewer manual breaks without false positives, and an LLM on every pair is neither affordable nor auditable. | Deterministic-first matching with LLM adjudication reserved for genuinely ambiguous pairs behind a cost-capped contract, persistent pair caching, human review, atomic runs with clean rollback, and a Go match-worker validated by replaying real Python-exported events. |
| **[REGLENS](https://github.com/roshanrana/RegLens)** · Python, FastAPI, SQLite, Qdrant | Compliance teams need answers they can cite, and a RAG system that paraphrases a rule is worse than no system. | Hybrid retrieval with exact-citation routing, quote verification against retrieved evidence, abstention on weak evidence, hash-chained query audits with reviewer-ready exports, durable chat sessions, and adversarial prompt-injection evals, all runnable offline. 268 tests. |
| **[MARKETSAGE](https://github.com/roshanrana/MarketSage)** · Go, Python, TypeScript, MCP, DuckDB | An analyst workflow exists; LLM clients want to use it. | A Go MCP gateway exposing seven finance tools and a saved-run resource over a FastAPI analytics core, DuckDB audit persistence, a Next.js workbench, seeded/hybrid/live data modes, and dependency and vulnerability sweeps run before release. |

## How they are built

The same way every time, because the way is the point.

**Design before code.** Requirements, a high-level design, a low-level design with frozen contracts, and a task-level execution plan, each approved before the next begins. In SHADOWBOOK no application code exists before the commit that approved the plan, and the git history shows it. Decisions are numbered and append-only, including the ones that were wrong.

**One gate.** `make check` runs format, lint, strict types, and tests, offline, with no broker, no database, no network and no API key. CI runs the same command and adds nothing to it.

**Deterministic by default, live by explicit act.** Every model, provider and external service sits behind an interface with a deterministic stand-in bound by default. Turning on the live path is a deliberate configuration change, never an accident of having a key in the environment.

**Adversarial fixtures with names.** Late files, redeliveries, four price columns, a trailer that lies about its total, a broker killed mid-payday. Each maps to a test whose name says what broke.

**Honest about what is not measured.** Every ship report has a section for what was written but never run, and the numbers in a README trace to committed raw output or they are not in the README.

## Background

Senior Implementation Specialist at NeoXam, embedded with investment-bank clients from first scoping call through production and hand-over. Before that, thirteen years deploying TLM Collateral, Reconciliations and AIR platforms into more than thirty banks across six continents for SmartStream and Algorithmics (IBM), and a year as an independent technical lead on FINRA 4210, T+1 and ISO 20022 programmes at MUFG and Mizuho. Off the clock: Ironman and ultramarathon distances, which turn out to be good training for cutover weekends.

[LinkedIn](https://www.linkedin.com/in/roshanrana/)
