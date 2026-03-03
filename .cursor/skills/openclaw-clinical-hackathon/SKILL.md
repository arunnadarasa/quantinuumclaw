---
name: openclaw-clinical-hackathon
description: Gets OpenClaw Clinical Hackathon participants started quickly with Quantinuum, Guppy, Selene, and Fly.io for clinical projects. Use when building clinical or healthcare applications with quantum computing, deploying quantum backends, or when the user mentions the hackathon, clinical use cases, drug discovery, treatment optimization, or patient stratification.
---

# OpenClaw Clinical Hackathon – Quick Start

This skill helps hackathon participants build **clinical applications** using **Quantinuum** (quantum hardware), **Guppy** (quantum language), **Selene** (backend API), and **Fly.io** (deployment). Use the existing quantum stack in this repo and map it to clinical use cases.

## When to Use This Skill

- User is in the OpenClaw Clinical Hackathon or building a clinical/healthcare project
- User wants to use Quantinuum, Guppy, Selene, or Fly.io for a demo or prototype
- User mentions: clinical, healthcare, drug discovery, treatment optimization, patient stratification, molecular simulation, clinical trials, medical data

## Stack at a Glance

| Component   | Role |
|------------|------|
| **Quantinuum** | Quantum hardware (H-series); use emulator for local dev |
| **Guppy**      | Quantum programming (circuits, gates, measurement) |
| **Selene**     | FastAPI backend that runs Guppy algorithms and exposes REST API |
| **Fly.io**     | Hosts the Selene backend in the cloud |

Frontend: use the Lovable template in `assets/lovable-template/` or any React/TS app that calls the Selene API.

## Quick Start (One Command)

From the repo root:

```bash
python3 scripts/create_quantum_app.py \
  --app-name "clinical-demo" \
  --use-case "chemistry" \
  --description "Clinical molecular simulation" \
  --deploy
```

Then set `VITE_API_URL` in the frontend to your Fly.io app URL (e.g. `https://clinical-demo.fly.dev`).

**Clinical use-case → `--use-case` mapping:**

| Clinical idea                     | `--use-case`  | Notes |
|-----------------------------------|---------------|--------|
| Drug discovery / molecular sim    | `chemistry`   | Molecules, energy, properties |
| Treatment / resource optimization | `optimization`| QAOA-style optimization |
| Patient stratification / ML       | `ml`          | Quantum ML models |
| Randomization (e.g. trials)       | `random`      | Quantum RNG |
| Secure keys / protocols           | `crypto`      | Quantum-safe crypto |

## Step-by-Step for Clinical Projects

### 1. Create the backend (Selene + Guppy)

```bash
python3 scripts/setup_selene_service.py \
  --app-name "my-clinical-app" \
  --use-case "chemistry" \
  --description "Drug discovery / molecular simulation"
```

This creates `my-clinical-app/` with FastAPI, health check, Dockerfile, and `fly.toml`.

### 2. Implement your clinical logic in Guppy

Edit `my-clinical-app/main.py` and implement `_run_real_quantum()` (and optionally keep `_run_mock_quantum()` for demos without hardware).

- **Chemistry / drug discovery:** parameterize molecule, shots, precision; call Guppy for energy or property estimation.
- **Optimization:** treatment scheduling, resource allocation → use the optimization template and map to your objective.
- **ML / stratification:** use the `ml` use case and map features to circuit parameters.

See `references/guppy_guide.md` for Guppy syntax and patterns.

### 3. Deploy to Fly.io

```bash
python3 scripts/flyio_deploy.py \
  --app-name "my-clinical-app" \
  --region "lhr"
```

Set secrets (e.g. Quantinuum API key) with `fly secrets set`; use emulator for hackathon if you prefer.

### 4. Frontend

Use `assets/lovable-template/` or run:

```bash
python3 scripts/lovable_integrate.py \
  --app-name "my-clinical" \
  --backend-url "https://my-clinical-app.fly.dev" \
  --quantum-use-case "chemistry"
```

Point the frontend’s API base URL to your Fly.io backend.

## Clinical Use Case Cheat Sheet

- **Drug discovery / molecular simulation:** `chemistry` — Guppy for VQE-style energy or property calculations; expose molecule type and parameters via the API.
- **Treatment or resource optimization:** `optimization` — define objective (e.g. cost, wait time); run quantum optimization (e.g. QAOA) in Selene; display results in the UI.
- **Patient stratification / classification:** `ml` — use quantum ML use case; map patient features to model inputs; return risk/stratum or classification.
- **Randomization (e.g. clinical trials):** `random` — use quantum RNG from Guppy for unbiased randomization; expose bits/shots in the API.
- **Security / key material:** `crypto` — use for key generation or quantum-safe primitives; keep keys and PHI only on backend, never in frontend.

## Data and Compliance (Hackathon)

- **Demos:** Use synthetic or de-identified data only. Do not send real PHI to quantum backends or store it in Fly.io without a clear compliance plan.
- **API keys:** Store Quantinuum (and other) keys in Fly.io secrets, not in code or frontend.
- **Frontend:** Call Selene only from your backend or from a frontend that does not send PHI to third parties; for production, add auth and consider HIPAA/DPA requirements.

## Key Paths in This Repo

| Resource | Path |
|----------|------|
| Guppy language reference | `references/guppy_guide.md` |
| Selene API (endpoints, errors, jobs) | `references/selene_api.md` |
| Fly.io (scaling, secrets, regions) | `references/flyio_config.md` |
| Frontend patterns (dashboard, API client) | `references/lovable_patterns.md` |
| Backend template (Dockerfile, fly.toml) | `assets/selene-template/` |
| Frontend template | `assets/lovable-template/` |
| Full app creator | `scripts/create_quantum_app.py` |
| Backend scaffold | `scripts/setup_selene_service.py` |
| Deploy to Fly.io | `scripts/flyio_deploy.py` |
| Frontend + backend URL | `scripts/lovable_integrate.py` |

## Troubleshooting

- **Guppy import error:** Install in backend env: `pip install guppy` (or use mock mode for demos).
- **Fly.io deploy fails:** Run `fly deploy --clean`; check `fly logs --phase build`; ensure `fly auth login` and valid `fly.toml` in app dir.
- **Frontend can’t reach API:** Confirm `VITE_API_URL` (or equivalent) is the Fly.io URL; ensure Selene CORS allows your frontend origin; hit `/health` with curl first.
- **Need faster iteration:** Use `QUANTUM_HARDWARE=emulator` and mock mode; deploy once to Fly.io then iterate on code and redeploy.

## Deeper Guidance

- For full quantum app workflow (non-clinical), see the repo root **SKILL.md** (quantum-guppy-selene).
- For clinical use-case details and example mappings, see [clinical-use-cases.md](clinical-use-cases.md) in this skill folder.
