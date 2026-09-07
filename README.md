# Roshan Rana

I take vendor platforms live inside large financial institutions. Eighteen years of it: collateral, payments, reconciliation, and now AI systems, always on the client's side of the change-control gate, always against a regulator's calendar rather than a project plan.

This is where I build in public. Every project here starts from an operational problem a bank would recognise, keeps AI bounded by evidence and human review, and ships with a deterministic path a reviewer can clone and verify in minutes. None of them are products. All of them are built to production constraints.

## Projects

Six systems. Each has an `OVERVIEW.md` (what it is and why) and a `SHOWCASE.md` (a guided tour of the features, with the commands to run) under `docs/`.

| | The problem | What it proves |
|---|---|---|
| **[SHADOWBOOK](https://github.com/roshanrana/shadowbook)** · Go, Python, PostgreSQL, Redpanda | Core-ledger migrations fail on the undocumented behaviour of the incumbent, not on the happy path. | A double-entry shadow ledger run alongside a legacy simulator carrying twelve seeded quirks, reconciled at three grains, with time-to-discovery measured per quirk. Delivery semantics measured against three real brokers killed mid-run: at-most-once both lost *and* duplicated. 243 tests; findings generated from artefacts, never hand-written. **12 of 12** seeded behaviours surfaced, median 84 transactions to the first break; [measured results](https://github.com/roshanrana/shadowbook#results). |
| **[HARBORMASTER](https://github.com/roshanrana/Harbormaster)** · Go, Python, Protobuf, Kafka, Postgres | Client, custodian and exchange files arrive under many names and formats; the reconciliation engine has to be told which client, which value date, and which of four price columns is the price. | Six event-driven services, a three-tier mapping ladder whose model dependence *decreases* as confirmed mappings promote into configuration, quarantine and four-eyes review, hash-chained audit, and twelve adversarial fixtures each with a named test. 379 tests; 100% attribution and value-date accuracy on the reference corpus. **97.7%** field-mapping accuracy on 214 labelled columns, **80.8%** resolved without a model; [measured results](https://github.com/roshanrana/Harbormaster#results). |
| **[PROVENANCE](https://github.com/roshanrana/PROVENANCE)** · Python, Go, vLLM, SGLang, llm-d, Kubernetes | A bank runs one shared LLM inference platform across an information barrier. Batched inference is not reproducible, and the cache-aware router leaks which prefixes other tenants have used. | Both halves measured. At temperature 0, **34 of 128** identical requests returned distinct logprob vectors; vLLM's batch-invariant mode leaves 5 and costs 22.7% of throughput — a figure confounded with the prefix cache it forces off, so a second engine supplies the missing cell of a 2×2 and the isolated cost is **18.0%**. The cross-tenant routing leak measures **AUC 1.0000** as a confirmation oracle and the tenant-salt plugin closes it to chance on the same schedule, both deployment profiles standing up in public CI on every push. Signed receipts anchor model identity to a Hugging Face commit and weight digest, connected to SR 11-7 validation. Pre-registered statistics, implemented rather than imported. 332 Python and 22 Go tests; [results with figures](https://github.com/roshanrana/PROVENANCE/blob/main/docs/RESULTS.md). |
| **[LEDGERLENS](https://github.com/roshanrana/LedgerLens)** · Python, Go, SQLite, Kafka | Reconciliation teams want fewer manual breaks without false positives, and an LLM on every pair is neither affordable nor auditable. | Deterministic-first matching with LLM adjudication reserved for genuinely ambiguous pairs behind a cost-capped contract, persistent pair caching, human review, atomic runs with clean rollback, and a Go match-worker validated by replaying real Python-exported events. **6 of 6** golden checks, 75% straight-through, 12 of 12 emitted events schema-conformant; [measured results](https://github.com/roshanrana/LedgerLens#results). |
| **[REGLENS](https://github.com/roshanrana/RegLens)** · Python, FastAPI, SQLite, Qdrant | Compliance teams need answers they can cite, and a RAG system that paraphrases a rule is worse than no system. | Hybrid retrieval with exact-citation routing, quote verification against retrieved evidence, abstention on weak evidence, hash-chained query audits with reviewer-ready exports, durable chat sessions, and adversarial prompt-injection evals, all runnable offline. 275 tests. Abstention **14.3%** with zero false abstentions, citation faithfulness **100%**; [measured results](https://github.com/roshanrana/RegLens#results). |
| **[MARKETSAGE](https://github.com/roshanrana/MarketSage)** · Go, Python, TypeScript, MCP, DuckDB | An analyst workflow exists; LLM clients want to use it. | A Go MCP gateway exposing seven finance tools and a saved-run resource over a FastAPI analytics core, DuckDB audit persistence, a Next.js workbench, seeded/hybrid/live data modes, and dependency and vulnerability sweeps run before release. |

## Measured, not claimed

Five of the six repositories carry a results card at the top of their README. Every number on it is written by an offline harness with a fixed seed, no network and no API key, into `metrics/headline.json`, and CI fails the build when the card drifts from the file. Anything that needs a GPU, a live model or a running cluster is listed on the card as *pending* rather than estimated.

| | Headline numbers | Harness |
|---|---|---|
| **[SHADOWBOOK](https://github.com/roshanrana/shadowbook#results)** | 12 of 12 seeded legacy behaviours surfaced; median 84 transactions, 2.5 business days, to the first break; 3 of 12 isolated to a single cause. One bar per behaviour, and breaks counted at all three reconciliation grains. | `make headline` |
| **[HARBORMASTER](https://github.com/roshanrana/Harbormaster#results)** | 97.7% field-mapping accuracy on 214 hand-labelled columns across 19 pinned files; 80.8% resolved without a model (alias 160, fuzzy 8, model 5); quarantine precision 100%, recall 66.7%; hash-chain tamper check fails closed. | `make bench` |
| **[PROVENANCE](https://github.com/roshanrana/PROVENANCE#results)** | Bootstrap interval coverage 91.0% over 200 null datasets; 8 components present on the tree; 4 of 11 published claims verifiable with no GPU, the other 7 recorded in `bench/results` and shown as pending. | `make headline` |
| **[LEDGERLENS](https://github.com/roshanrana/LedgerLens#results)** | 6 of 6 golden checks on the sample replay; 75% matched straight through, 25% routed to review; 12 of 12 emitted events conform to the JSON Schema contracts. | `make golden` |
| **[REGLENS](https://github.com/roshanrana/RegLens#results)** | Abstention 14.3% with zero false abstentions on 21 fixture queries; citation faithfulness 100%; recall@5 100% (n=18); reranker on versus off measured at every k. | `make eval` |
| **[MARKETSAGE](https://github.com/roshanrana/MarketSage)** | No harness yet; scoping first. | |

## How they are built

The same way every time, because the way is the point.

**Design before code.** Requirements, a high-level design, a low-level design with frozen contracts, and a task-level execution plan, each approved before the next begins. In SHADOWBOOK no application code exists before the commit that approved the plan, and the git history shows it. Decisions are numbered and append-only, including the ones that were wrong.

**One gate.** `make check` runs format, lint, strict types, and tests, offline, with no broker, no database, no network and no API key. CI runs the same command and adds nothing to it.

**Deterministic by default, live by explicit act.** Every model, provider and external service sits behind an interface with a deterministic stand-in bound by default. Turning on the live path is a deliberate configuration change, never an accident of having a key in the environment.

**Adversarial fixtures with names.** Late files, redeliveries, four price columns, a trailer that lies about its total, a broker killed mid-payday. Each maps to a test whose name says what broke.

**Honest about what is not measured.** Every ship report has a section for what was written but never run, and the numbers in a README trace to committed raw output or they are not in the README. In PROVENANCE that stopped being a convention and became a test: every published figure lives once in a JSON file, the charts are generated from it, and the build fails when a document drifts away from it or quotes a confounded number without saying so.

## Background

Senior Implementation Specialist at NeoXam, embedded with investment-bank clients on their hours and time zones, from first scoping call through production and hand-over. Before that, thirteen years deploying TLM Collateral, Reconciliations and AIR platforms into more than thirty banks across six continents for SmartStream and Algorithmics (IBM), and a year as an independent technical lead on FINRA 4210, T+1 and ISO 20022 programmes at MUFG and Mizuho. Off the clock: Ironman and ultramarathon distances, which turn out to be good training for cutover weekends.

[LinkedIn](https://www.linkedin.com/in/roshanrana/)
