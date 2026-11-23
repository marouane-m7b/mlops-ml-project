## What
-

## Why
-

## How to test
```bash
source .venv/bin/activate
uv pip sync requirements-lock.txt
python -m pytest -q
python scripts/train.py
```

## Proof (métriques)
- metrics.json avant :
- metrics.json après :

## Checklist
- [ ] Tests OK
- [ ] Pas de data/ ni artifacts/ commités
- [ ] README à jour si nécessaire
