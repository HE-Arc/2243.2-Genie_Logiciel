---
title: "4 - Modélisation Fonctionnelle"
type: docs
weight: 10
---
# Chapitre 4 : Modélisation Fonctionnelle

## Slides
{{< pdf src="/pdfs/2243.2_04_ModelisationFonctionnelle.pdf" >}}

## Exercices

### Exercice 1 : Diagramme de cas d'utilisation (Use Case Diagram)
Nous souhaitons modéliser un système pour gérer les cours et les inscriptions.
Un étudiant peut s’inscrire à un cours et consulter ses notes.
Un professeur peut publier les notes.
Un administrateur gère les comptes utilisateurs et valide les inscriptions.
Le secrétariat est un cas particulier d’administrateur, limité à la validation des inscriptions.

**Produire le diagramme de cas d’utilisation UML**

{{< plantuml  id="UC1">}}
  @startuml
left to right direction

actor Student as Student
actor Professor as Prof
actor Administrator as Admin
actor "Secretariat" as Sec
Sec <|-- Admin  

rectangle "System" as System {
  usecase "Enroll in course" as UC_Enroll
  usecase "View grades" as UC_ViewGrades

  usecase "Publish grades" as UC_Publish

  usecase "Manage user accounts" as UC_Accounts
  usecase "Validate enrollment" as UC_Validate
}

Student --> UC_Enroll
Student --> UC_ViewGrades

Prof --> UC_Publish

Admin --> UC_Accounts
Sec --> UC_Validate

UC_Enroll --> UC_Validate : includes
UC_Publish --> UC_Validate : includes
UC_ViewGrades --> UC_Publish : includes

@enduml
{{< /plantuml >}}


### Exercice 2 : Diagramme de séquence système
En utilisant le même contexte que l’exercice 1, nous souhaitons modéliser le scénario d’inscription à un cours avec validation différée par l’administration (Administrateur ou Secrétariat).

Le scénario principal est le suivant :

1. **Inscription avec validation différée**
* L’Étudiant s’authentifie.
* Il demande l’inscription à un cours `courseId`.
* Le Système vérifie les prérequis et la capacité.
* Le Système place l’inscription en **“En attente”** et **notifie** l’Administrateur (ou le Secrétariat).
* Le Système confirme à l’Étudiant que la demande est enregistrée.

 **Produire le **DSS** correspondant.**

{{< plantuml  id="DSS1">}}
@startuml
!pragma teoz true
title Demande d'inscription à un cours

actor Etudiant as Student
participant "Système" as System
actor "Administration" as AdminGeneric

== Authentification ==
Student -> System: authenticate(credentials)
System --> Student: authOK

== Demande d'inscription ==
Student -> System: requestEnrollment(courseId)
activate System

alt Prérequis OK et places disponibles
  System -> Student: enrollmentRecorded(status="pending")
  System -> AdminGeneric: notifyPendingEnrollment(studentId, courseId)
else Prérequis non satisfaits
  System -> Student: rejection(reason="missing prerequisites")
else Cours complet
  System -> Student: waitlisted()
end

deactivate System
@enduml
{{< /plantuml >}}

2. **Validation de l’inscription par l’Administration**
* L’Administrateur (ou le Secrétariat) s’authentifie.
* Il/elle **valide** l’inscription de l’Étudiant au cours.
* Le Système **confirme** la validation et **notifie** l’Étudiant.

 **Produire le **DSS** correspondant.**

{{< plantuml id="DSS2">}}
@startuml
!pragma teoz true
title Validation d'inscription (niveau système)

actor Administrateur as Admin
actor Secretariat as Sec
participant "Système" as System
actor Etudiant as Student

alt Initié par Administrateur
  Admin -> System: authenticate(credentials)
  System --> Admin: authOK
  Admin -> System: validateEnrollment(studentId, courseId)
  activate System
  System --> Admin: validationConfirmed()
  System -> Student: notifyEnrollmentValidated(courseId)
  deactivate System
else Initié par Secrétariat
  Sec -> System: authenticate(credentials)
  System --> Sec: authOK
  Sec -> System: validateEnrollment(studentId, courseId)
  activate System
  System --> Sec: validationConfirmed()
  System -> Student: notifyEnrollmentValidated(courseId)
  deactivate System
end

alt Rejet de la demande (ex: dossier incomplet)
  Admin -> System: rejectEnrollment(studentId, courseId, reason)
  activate System
  System --> Admin: rejectionRecorded()
  System -> Student: notifyEnrollmentRejected(reason)
  deactivate System
end
@enduml
{{< /plantuml>}}

### Exemple de DSS "atypique"
Le diagramme suivant illustre un workflow complet pour la soumission d’un article à une conférence scientifique, incluant le dépôt sur arXiv et la gestion des artefacts (code et données).
Ce DSS met en évidence les interactions entre l’auteur, le système de soumission, arXiv, les dépôts de code/données, et les services d’indexation.
Il est intéressant car il montre que l'UML peut aussi être utilisé pour modéliser des processus métier complexes, pas seulement des interactions techniques entre systèmes.

{{< plantuml id="DSS_arXiv">}}
@startuml
title Workflow "Soumission conférence + dépôt arXiv" (DSS)

actor "Auteurs" as Auteur
participant "Règlement\nde la\n conférence" as Policy
participant "Système\nde\nsoumission" as Conf
participant "arXiv" as Arxiv
participant "Code\n&\nDonnées" as CodeRepo
participant "Indexation" as Index

== Préparation ==
Auteur -> Auteur: Rédige le manuscrit
Auteur -> Auteur: Prépare artefacts\n(code/données, README, LICENSE)
note over Auteur,CodeRepo: Vérifier anonymisation (double-blind)\n→ pas de noms/affiliations/DOI internes

== Vérification des règles ==
Auteur -> Policy: Lire règles\n(preprint, double-blind, prior-publi.)
Policy --> Auteur: Règles lues

alt Preprints autorisés (cas courant en ML/Graphics)
  opt Dépôt arXiv AVANT/À LA SOUMISSION
    Auteur -> Arxiv: Déposer v1 (titre, auteurs, catégorie)\n+ lien code (optionnel)
    Arxiv --> Auteur: ID arXiv et timestamp
    Auteur -> CodeRepo: Publier repo (public ou privé)\n+ Release (optionnel)
    CodeRepo -> Index: Créer DOI\nvia Zenodo\n(optionnel)
  end
else Preprints NON autorisés / domaine sensible
  Auteur -> Auteur: Reporter le dépôt arXiv\n(jusqu’après review/acceptation)
end

== Soumission ==
Auteur -> Conf: Soumettre papier (PDF + suppl.)
Conf --> Auteur: Accusé réception

opt Processus double-blind
  note over Auteur,Conf: Éviter de relier publiquement arXiv/GitHub\nà l’identité durant la review
end

== Décision ==
Conf --> Auteur: Décision (accepté / refusé)

alt Accepté
  Auteur -> Auteur: Préparer camera-ready\n(révisions, métadonnées)
  Auteur -> Conf: Soumettre version finale + droits
  opt Mise à jour arXiv après acceptation
    Auteur -> Arxiv: Mettre à jour v2\n(\"Accepted at <Conf, Année>\")\n+ ajouter DOI officiel quand disponible
    Arxiv --> Index: Ré-indexation
  end
  opt Artefacts reproductibles
    Auteur -> CodeRepo: Rendre public le code/données\n+ tag release, archiver\n(vers Zenodo + DOI)
    CodeRepo --> Index: Indexation\n(badges, PWCode)
  end
else Refusé
  opt Révision et re-soumission
    Auteur -> Auteur: Réviser manuscrit
    opt Dépôt/MAJ arXiv
      Auteur -> Arxiv: Mettre à jour (v2/v3) avec changelog
    end
    Auteur -> Conf: Soumettre à une autre conf./journal
  end
end

== Communication et traçabilité ==
opt Métadonnées et profils
  Auteur -> Index: Mettre à jour profils\n(Google Scholar, ORCID)
end

== Bonnes pratiques (rappels) ==
hnote over Auteur
- Cohérence entre versions (soumise, arXiv, camera-ready)
- Respect de l’anonymat pendant review
- Mention claire: "Accepted at <Conf, Year>" après acceptation
- Ajouter DOI éditeur sur arXiv dès disponibilité
- Licence claire pour code/données (MIT/Apache/CC)
end note

@enduml
{{< /plantuml >}}