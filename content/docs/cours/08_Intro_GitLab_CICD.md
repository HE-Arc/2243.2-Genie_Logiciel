---
title: "8 - Introduction à GitLab CICD"
type: docs
weight: 10
---
# Chapitre 8 : Introduction à GitLab CICD

## Slides

{{<slides "https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/08_Intro_GitLab_CICD.html">}}

[Version imprimable (faire CTRL+P)](https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/08_Intro_GitLab_CICD.html?print-pdf)

## Exercices

### Exercice 1 : intégration
Mettre en place un pipeline GitLab CI/CD simple pour compiler et tester un projet C++ hébergé sur un dépôt GitLab. Le pipeline doit inclure les étapes suivantes :
1. **Génération du système de build** : utiliser CMake pour générer les fichiers de build.
2. **Compilation** : utiliser Ninja pour compiler le projet.
3. **Tests** : lancer l'exécutable.