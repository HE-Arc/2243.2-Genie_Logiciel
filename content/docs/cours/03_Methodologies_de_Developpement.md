---
title: "3 - Méthodologies de Développement"
type: docs
weight: 10
---
# Chapitre 3 : Méthodologies de Développement

## Slides
{{<slides "https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/03_Methodologies_de_developpement.html">}}

[Version imprimable (faire CTRL+P)](https://he-arc.github.io/2243.2-Genie_Logiciel-SLIDES/03_Methodologies_de_developpement.html?print-pdf)

## Méthodologies de développement

### Waterfall (cascade)
{{< plantuml id="Waterfall" >}}
@startuml
title Waterfall (phases et retours depuis la maintenance)
actor "Client" as C
participant "Analyse" as AN
participant "Conception" as DE
participant "Implémentation" as IM
participant "Test\n&\nIntégration" as IT
participant "Maintenance" as MA

C -> AN : Cahier des charges
AN -> DE : Spécifications détaillées
DE -> IM : Diagrammes de classes, etc.
IM -> IT : Code
IT -> MA : Déploiement

note over C, MA : 1er retours client après des mois, voire des années, de développement


alt Besoins mal compris
  MA --> AN : Retour à l'analyse
else Erreur de conception
  MA --> DE : Retour à la conception
else Défaut d'implémentation
  MA --> IM : Retour au code
else Défaut d'intégration
  MA --> IT : Retour aux tests
end
note over C, MA : Chaque retour redescend toute la cascade à partir de la phase touchée
@enduml
{{< /plantuml >}}

### Modèle en V
{{< plantuml id="ModeleEnV" >}}
@startuml
title Modèle en V (chaque phase de conception prépare ses tests)
actor "Client" as C
participant "Analyse" as AN
participant "Conception" as DE
participant "Implémentation" as IM
participant "Test\n&\nIntégration" as IT
participant "Maintenance" as MA

C -> AN : Cahier des charges
AN -> IT : Plan des tests de validation
AN -> DE : Spécifications détaillées
DE -> IT : Plan des tests d'intégration
DE -> IM : Diagrammes de classes, etc.
IM -> IT : Code et tests unitaires
IT -> MA : Déploiement

note over C, MA : 1er retours client après des mois, voire des années, de développement


alt Échec des tests unitaires
  IT --> IM : Retour au code
else Échec des tests d'intégration
  IT --> DE : Retour à la conception
else Échec des tests de validation
  IT --> AN : Retour à l'analyse
end
note over C, MA : Différence avec la cascade : les tests sont préparés pendant la descente, et chaque échec renvoie à la phase qui a écrit le test
@enduml
{{< /plantuml >}}

## Développement Agentique

{{< plantuml id="DevAgentique" >}}
@startuml
title Développement agentique (une fonctionnalité à la fois, l'humain valide chaque étape)
actor "Client" as C
participant "Analyse" as AN
participant "Conception" as DE
participant "Implémentation" as IM
participant "Test\n&\nIntégration" as IT
participant "Maintenance" as MA

C -> AN : Cahier des charges
loop Pour chaque fonctionnalité
  AN -> IT : Scénarios d'acceptation (Gherkin)
  AN -> DE : Spécifications détaillées (EARS)
  DE -> IM : Diagrammes de classes, etc.
  note over AN, DE : Humain : vérifie et valide spécifications et conception
  IM -> IT : Code (MR/PR depuis un git worktree)
  note over IM : Agent code
  note over IT : Agent tests\nAgent qualité (mesure)\nAgent revue et gestion

  alt Échec des tests unitaires
    IT --> IM : Retour au code
  else Échec des tests d'intégration
    IT --> DE : Retour à la conception
  else Échec des tests de validation
    IT --> AN : Retour à l'analyse
  end

  note over IM, IT : Humain : vérifie et valide la MR/PR
  IT -> MA : Déploiement
  MA --> C : Fonctionnalité livrée
end

note over C, MA : 1er retours client dès la première fonctionnalité
note over C, MA : Différence avec le V : chaque phase est tenue par un agent, et l'humain ne code plus, il vérifie et valide
@enduml
{{< /plantuml >}}


## Guide Scrum (à lire)
{{< pdf src="/pdfs/scrum-guide-fr.pdf" >}}

