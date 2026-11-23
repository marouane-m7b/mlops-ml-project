# mlops-ml-project — baseline ML reproductible

Projet de classification Iris avec une régression logistique. La configuration
est définie dans `config/train.yaml` ; les modules réutilisables sont dans `src/`
et les points d'entrée dans `scripts/`.

## Installation (Linux / macOS)

Prérequis : Python 3.11 (version utilisée pour la baseline), uv et Git.
Exécuter les commandes depuis la racine du projet.

```bash
# Uniquement si .venv n'existe pas encore :
uv venv --python 3.11 .venv

source .venv/bin/activate
uv pip sync requirements-lock.txt
```

Réutiliser l'environnement `.venv` s'il existe déjà. `requirements.txt` déclare
les dépendances du projet ; `requirements-lock.txt` enregistre les versions
exactes utilisées pour cette baseline. Pour installer les dépendances sans
imposer ces versions : `uv pip install -r requirements.txt`.

## Entraînement

```bash
python scripts/train.py
cat artifacts/metrics.json
```

La baseline utilise Iris, un découpage stratifié avec `test_size: 0.2` et
`random_state: 42`, une imputation médiane et une standardisation.
Les métriques obtenues sur les 30 observations du jeu de test sont :
accuracy = 0.9333333333333333 et f1_macro = 0.9333333333333332.

## Évaluation

```bash
python scripts/evaluate.py
cat artifacts/report.json
```

Lancer l'entraînement avant l'évaluation pour créer le modèle. Dans la version
actuelle du TP, `evaluate.py` produit un rapport sur les 150 observations d'Iris,
y compris celles utilisées pour entraîner le modèle. Son accuracy de
0.9533333333333334 ne constitue donc pas une mesure indépendante de généralisation.

## Tests

```bash
python -m pytest -q
```

Les trois tests vérifient les sections obligatoires de la configuration, la
validité de `test_size` et la présence de données avec des tailles X/y cohérentes.

## Artefacts (générés dans artifacts/, non versionnés)

- `model.joblib` : pipeline entraîné (prétraitement + modèle).
- `metrics.json` : accuracy et f1_macro sur le jeu de test.
- `confusion_matrix.png` : matrice de confusion sur le jeu de test.
- `report.json` : rapport de classification détaillé sur l'ensemble d'Iris.

Les dossiers `data/`, `artifacts/` et `.venv/` sont exclus par `.gitignore`.
Le code, la configuration, les tests et la documentation sont versionnés.
