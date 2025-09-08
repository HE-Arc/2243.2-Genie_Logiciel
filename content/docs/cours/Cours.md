---
title: "Cours"
type: docs
weight: 10
---
# Cours

## Organisation du Cours

{{< pdf src="/pdfs/2243.2_00_OrganisationDuCours.pdf" >}}

## Chapitre 1

{{< pdf src="/pdfs/2243.2_01_Introduction.pdf" >}}

## Chapitre 2

{{< pdf src="/pdfs/2243.2_02_Cycle_de_vie_logiciel.pdf" >}}

## Chapitre 3

{{< pdf src="/pdfs/2243.2_03_MéthodologiesDeDéveloppement.pdf" >}}

{{< pdf src="/pdfs/scrum-guide-fr.pdf" >}}

## Chapitre 4

{{< pdf src="/pdfs/2243.2_04_ModélisationFonctionnelle.pdf" >}}

### Squelette de fichier plantuml UC

```plaintext
@startuml Chap4_UC_Example
left to right direction

' ACTORS
actor "Visiteur" as Visitor
actor "Membre" as Member
actor "Admin" as Admin

' USE CASES AND SYSTEM
' WARNING: { on same line as rectangle keyword
rectangle WebAPP { 
    usecase "Créer un compte" as Register
    usecase "Connexion" as Login
    usecase "Créer du contenu" as Create
    usecase "Publier du contenu" as Publish
    usecase "Bannir un compte" as Ban
}

' RELATIONSHIPS BETWEEN ACTORS
Visitor <|-- Member
Member <|-- Admin

' RELATIONSHIPS BETWEEN USE CASES
Register -> Login : extends
Publish -> Create : includes

' RELATIONSHIPS BETWEEN ACTORS AND USE CASES
Visitor -> Login
Member -> Publish
Admin -> Ban

@enduml
```

### Squelette de fichier plantuml DSS

```plaintext
@startuml DSSExampleGroups
actor Guest
actor Member
participant System

loop until correct
alt Wrong Password
Guest -> System: Authenticate
activate Guest
activate System
Guest <-- System: ERROR
else Correct credentials
Guest -> System: Authenticate
deactivate Guest
Member <-- System: OK
activate Member
end
end

deactivate System
activate Member
Member -> System: Edit Event
activate System
Member <-- System: Event Edited
deactivate System
deactivate Member

@enduml
```

## Chapitre 5

{{< pdf src="/pdfs/2243.2_05_ModélisationStructurelle.pdf" >}}

### Exemple de fichier plantuml

```plaintext
@startuml RelationExample
skinparam classAttributeIconSize 0
'left to right direction
hide circle

'Classes definitions
class Person
{    
    +FirstName : String
    +LastName : String
}

class Student
{    
    +ID : Integer
}

class Teacher
{
    +Email : String
}

class ResearchTeam
{
    +Name : String
    +Topics : List<String>    
}

class ResearchLab
{
    +Name : String
}

class Department
{
    +Name : String
}

'Relationships
Student --|> Person
Person ^-- Teacher
ResearchTeam "*" o- "1..*" Teacher : researchers
Department "1" o- "1..*" Teacher : teachers
ResearchLab "1" *- "1..*" ResearchTeam : teams

@enduml
```

Ce qui donne le diagramme suivant :
{{< figure src="/images/RelationExample.svg#center" width="100%">}}

## Chapitre 6

{{< pdf src="/pdfs/2243.2_06_ConceptionDynamique.pdf" >}}

### Exemple de fichier PlantUML
```
@startuml

state "En attente de papier" as NeedPaper
state "En attente d'encre" as NeedToner
state Impression : Do : imprime
state NeedPaper : Do : Afficher erreur
state NeedToner : Do : Afficher erreur

[*] --> Éteinte
Éteinte --> Allumée : Mise en marche
Allumée --> Impression : Print
Impression --> Allumée : Doc. Imprimé [Encre OK]
Impression --> NeedPaper : Plus de papier
Impression --> NeedToner : Doc. Imprimé [Encre manquante]
Allumée --> NeedPaper : Plus de papier
NeedPaper  --> Allumée : Papier ajouté
Allumée --> NeedToner : Plus d'encre
NeedToner   --> Allumée : Cartouche remplacée
NeedToner   --> Impression : Print
Allumée --> Éteinte : Mise hors tension

@enduml
```

Ce qui donne le diagramme suivant :
{{< figure src="/images/DiagrammeEtats.svg#center" width="100%">}}

## Chapitre 7 : NINJA & CMAKE
{{< pdf src="/pdfs/2243.2_07_IntroCMakeEtNinja.pdf" >}}

### Exemple de projet CMake

## Chapitre 8 : INTÉGRATION CONTINUE
{{< pdf src="/pdfs/2243.2_08_IntroGitLab_CICD.pdf" >}}

## Chapitre 9 : Introduction à GIT (rappels)
{{< pdf src="/pdfs/2243.2_09_Git_Intro.pdf" >}}

## Chapitre 10 : GIT, partie 2
{{< pdf src="/pdfs/2243.2_10_Git_Part2.pdf" >}}

## Chapitre 11 : GIT, partie 3
{{< pdf src="/pdfs/2243.2_11_Git_Part3.pdf" >}}

## Chapitre 12 : GIT, partie 4
{{< pdf src="/pdfs/2243.2_12_Git_Part4.pdf" >}}

## Contrôles Principaux (CP)

### 2023-2024
{{< pdf src="/pdfs/CPs/2023-2024_CP.pdf" >}}

### 2022-2023
{{< pdf src="/pdfs/CPs/2022-2023_CP.pdf" >}}

### 2021-2022
{{< pdf src="/pdfs/CPs/2021-2022_CP.pdf" >}}
