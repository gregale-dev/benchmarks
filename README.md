# Gregale Benchmarks & Reproducible Studies

Public benchmark datasets, verification scripts, and runnable fixtures from [Gregale](https://gregale.dev) infrastructure studies.

> **Note:** This repository publishes benchmark data, analysis scripts, and sample fixtures. The Gregale platform itself is proprietary software.

## Published studies

| Study | Date measured | Key result | Verify locally | Canonical report |
|---|---|---|---|---|
| **Cloud agent-ops guardrails matrix (8 PaaS platforms)** | 2026-11-25 | 8 platforms scored across 8 coding-agent safety controls (16-pt rubric): Gregale 16/16, Google Cloud Run 8/16, Vercel 6/16, Fly.io / Northflank / Render 5/16, Koyeb / Railway 3/16 | `python3 agent-ops-guardrails-matrix-2026-11-25/analyze.py --verify` | [Read report](https://gregale.dev/research/agent-ops-guardrails-matrix-2026-11-25) |
| **Cross-platform intermittent & evenly spaced API cost model** | 2026-11-25 | ~1–2 s `between_requests` pause ladder vs 5–30 min sleep timers across 6 PaaS platforms: Gregale Hobby ($10/mo for 5 evenly spaced 24/7 services + Postgres) vs $22.45–$41.00 always-on; continuous 2 req/s favors Fly/Railway/Heroku/Render | `python3 paas-intermittent-api-cost-model-2026-11-25/analyze.py --verify` | [Read report](https://gregale.dev/research/paas-intermittent-api-cost-model-2026-11-25) |
| **Intermittent FastAPI compute cost** | 2026-11-24 | Burst traffic used **42.9% less billable compute** than spread traffic for the same 8 requests (2,112 vs 3,696 MB-seconds; 0.086 vs 0.150 GB-RAM-h projected at 40 req/day) | `python3 intermittent-fastapi-cost-2026-11-24/analyze.py --verify` | [Read report](https://gregale.dev/research/intermittent-fastapi-cost-2026-11-24) |
| **Firecracker snapshot restore on SSD** | 2026-09-09 | 100 sequential snapshot restores on an SSD-backed node: **94.795 ms p50**, **137.756 ms p95**, **149.067 ms max** (`wake.boot_started` → `wake.boot_completed`; 0 samples ≥ 350 ms) | `python3 firecracker-snapshot-restore-ssd-2026-09-09/analyze.py --verify` | [Read report](https://gregale.dev/research/firecracker-snapshot-restore-ssd-2026-09-09) |

## Quick verification

Every check uses Python 3.11+ and the Python standard library only (no third-party packages required):

```sh
python3 agent-ops-guardrails-matrix-2026-11-25/analyze.py --verify
python3 paas-intermittent-api-cost-model-2026-11-25/analyze.py --verify
python3 intermittent-fastapi-cost-2026-11-24/analyze.py --verify
python3 firecracker-snapshot-restore-ssd-2026-09-09/analyze.py --verify
```

## Machine-readable Gregale endpoints

- Agent index: [`https://gregale.dev/llms.txt`](https://gregale.dev/llms.txt) ([core subset](https://gregale.dev/llms-small.txt), [full](https://gregale.dev/llms-full.txt))
- Plans & pricing JSON: [`https://gregale.dev/pricing.json`](https://gregale.dev/pricing.json)
- OpenAPI specification: [`https://gregale.dev/openapi.yaml`](https://gregale.dev/openapi.yaml) ([JSON](https://gregale.dev/openapi.json))
- Atom feed (articles & research): [`https://gregale.dev/feed.xml`](https://gregale.dev/feed.xml)
- Hosted Management MCP server (preview): `https://api.gregale.dev/mcp` ([MCP server card](https://gregale.dev/.well-known/mcp/server-card.json))

## Repository layout

- `agent-ops-guardrails-matrix-2026-11-25/` — Guardrail rubric (`criteria.json`), sourced evaluations (`vendors.json`), deterministic scorer (`analyze.py`), and `summary.json`.
- `paas-intermittent-api-cost-model-2026-11-25/` — Published vendor pricing inputs (`vendors.json`), 4 backend workload scenarios (`scenarios.json`), deterministic `Decimal` calculator (`analyze.py`), and `summary.json`.
- `intermittent-fastapi-cost-2026-11-24/` — FastAPI fixture (`gregale.yaml`, `main.py`, `requirements.txt`), traffic/state/ledger captures, pricing snapshot, and `analyze.py` / `run.py`.
- `firecracker-snapshot-restore-ssd-2026-09-09/` — 100-sample scheduler restore CSV (`samples.csv`), `summary.json`, and `analyze.py`.
