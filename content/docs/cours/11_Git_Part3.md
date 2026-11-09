---
title: "11 - Git : sous le capot et travail en parallèle"
type: docs
weight: 20
---
# Chapitre 11 : Git, sous le capot et travail en parallèle

## Slides

{{<slides "https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/11_Git_Internes_et_Worktrees.html">}}

[Version imprimable (faire CTRL+P)](https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/11_Git_Internes_et_Worktrees.html?print-pdf)

## Exercices

### Exercice 1 : worktrees
Par groupe de 2, sur votre repo GitLab :
1. Créer une branche `<Dev>_<Id>_Feature`, faire un commit, puis laisser une modification **non commitée**.
2. Un bug urgent arrive : créer un worktree `../<repo>-hotfix` avec une branche `hotfix` partant de `main`.
3. Dans le worktree : corriger, commit, fusionner dans `main`, push.
4. Supprimer le worktree et la branche `hotfix`.
5. Revenir dans le dossier principal : la modification non commitée est toujours là. Rebaser la feature sur `main`.
