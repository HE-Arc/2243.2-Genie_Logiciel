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

<!--
{{< plantuml  id="UC1">}}
  @startuml
left to right direction

actor Student as Student
actor Professor as Prof
actor Administrator as Admin
actor "Secretariat" as Sec
Admin <|-- Sec  

rectangle "System" as System {
  usecase "Enroll in course" as UC_Enroll
  usecase "View grades" as UC_ViewGrades

  usecase "Publish grades" as UC_Publish

  usecase "Manage user accounts" as UC_Accounts
  usecase "Validate enrollment" as UC_Validate

  usecase "Authenticate" as UC_Auth
}

Student --> UC_Enroll
Student --> UC_ViewGrades

Prof --> UC_Publish

Admin --> UC_Accounts
Admin --> UC_Validate
Sec --> UC_Validate

UC_Enroll       --> UC_Auth : includes
UC_ViewGrades   --> UC_Auth : includes
UC_Publish      --> UC_Auth : includes
UC_Accounts     --> UC_Auth : includes
UC_Validate     --> UC_Auth : includes

UC_Enroll --> UC_Validate : includes

@enduml
{{< /plantuml >}}
-->

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

 <!-- {{< plantuml  id="DSS1">}}
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
{{< /plantuml >}} -->

2. **Validation de l’inscription par l’Administration**
* L’Administrateur (ou le Secrétariat) s’authentifie.
* Il/elle **valide** l’inscription de l’Étudiant au cours.
* Le Système **confirme** la validation et **notifie** l’Étudiant.

 **Produire le **DSS** correspondant.**

<!-- {{< plantuml id="DSS2">}}
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
{{< /plantuml>}} -->
