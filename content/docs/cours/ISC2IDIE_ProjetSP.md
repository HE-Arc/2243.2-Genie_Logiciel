---
title: "ISC2IDIE - Projet SP"
type: docs
weight: 30
---
# ISC2IDIE - Projet SP
Durant ce semestre, vous devrez réaliser un projet en C++ dans le cadre du cours de Génie Logiciel 2.
Il faudra appliquer les concepts vus durant le semestre précédent (CI/CD, tests unitaires, documentation, gestion de versions avec Git, etc.).
Le projet se fera en groupe de 3–4 étudiants.

## Évaluation Génie Logiciel 2 (ISC2IDIE)
Vous serez évalués sur les critères suivants :
- Conception et architecture du code (diagrammes UML)
- Utilisation du Git rebase workflow
- Utilisation de Pull Requests pour les contributions
- CI/CD
- CMake + Ninja
- Doxygen (avec homepage)
- Unit tests (avec utilisation)
- GitLab (issues, milestones, wiki)
- Qualité générale

## Livrables
- Repository Git
- README technique
- Présentation finale

## Idées de projets
Voici quelques idées de projets possibles.

### Package Python simple implémenté en C++
- Bibliothèque C++ simple (vecteurs 3D, matrices, quaternions, etc.)
- Bindings C++ → Python
- Vectorisation
- Comparaison de performances (Python pur, C++, packages existants)

### Dataflow processing
Framework de Dataflow Processing (DAG + dirty flags + lazy update)
Construire un mini-framework C++ permettant de définir un pipeline de calcul sous forme de graphe orienté acyclique (DAG).
Chaque nœud représente une opération (transformations, agrégations, features, etc.) avec des dépendances explicites.
Voir Airflow, Prefect, Dagster.

### Framework de simulation de capteurs temps-réel
- Bruit gaussien, bruit intempestif, dérive, fréquence variable
- Producteurs / consommateurs asynchrones avec buffers circulaires
