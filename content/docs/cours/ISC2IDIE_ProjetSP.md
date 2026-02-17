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
- Bibliothèque C++ simple (matrices 4x4, quaternions, etc.)
- Tests unitaires en C++ avec Google Test (vs Eigen ou similaire)
- Bindings C++ → Python
- Vectorisation : pourquoi c'est plus rapide que des boucles Python ?
- Comparaison de performances (Python pur, C++, packages existants)

### Dataflow processing
Framework de Dataflow Processing (DAG + dirty flags + lazy update)
Construire un mini-framework C++ permettant de définir un pipeline de calcul sous forme de graphe orienté acyclique (DAG).
Chaque nœud représente une opération (transformations, agrégations, features, etc.) avec des dépendances explicites.
Voir Airflow, Prefect, Dagster.

### Cours portfolio
Voir https://rs.he-arc.ch/ mais transformé en un portfolio de cours comme pour le portfolio d'imagerie. Avec un graphe liant les différentes compétences, techniques, outils utilisés avec le niveau de maitrise acquis (débutant, intermédiaire, avancé).

1. Scrap pdfs depuis le site
2. Extraire les informations, pour chaque cours (testé, ça fonctionne à 90%)
3. Uniformiser les données pour chaque cours + corrections
4. Mise en forme (json, yaml, etc.). Les fichiers deviendront la base de données de référence
5. Générer un site static : une page, un cours, avec les tags associés.
1241.1 Langage C : <1ère année> <SA> <ISC> <Langage C>
Voir https://he-arc.github.io/imagerie-portfolio/
6. Pour chaque ajout / modification, lancer tous les tests pour vérifier que la nouvelle version respecte toutes les contraintes demandés (nommage, code cours, etc.)
7. Créer une graph des compétences avec difficulté, dépendances, etc.

#### Workflow

##### One-shot

Site web → PDFs → fichiers texte

##### CICD

→ fichiers texte → génération markdown (Hugo) → génération site web statique → Génération graphe de compétences

### Framework de simulation de capteurs temps-réel
- Bruit gaussien, bruit intempestif, dérive, fréquence variable
- Producteurs / consommateurs asynchrones avec buffers circulaires
