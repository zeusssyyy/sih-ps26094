# SIH PS-26094 — Soham's services

| Service | What | Port |
|---|---|---|
| services/risk-engine | /v1/fusion + /v1/forecast (FastAPI) | 8200 |
| services/web/victim | victim PWA (Vite + React) | 5173 |
| services/web/counsellor | counsellor console | 5174 |

## Run order
1. cd services/risk-engine
2. python -m venv .venv && source .venv/bin/activate   (Windows: .venv\Scripts\activate)
3. pip install -r requirements-dev.txt
4. pytest -q                          # gate: 7 passed
5. python -m training.calibrate_fusion  # gate: CALIBRATED
6. python -m training.train_forecaster  # gate: AUC >= 0.75
7. uvicorn app.main:app --port 8200
8. Web apps: npm install && npm run dev

## Important
services/risk-engine/artifacts/ IS committed to git — Avik's compose
mounts it into the container. Do not gitignore it.
