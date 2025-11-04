---
title: "5 - Modélisation Structurelle"
type: docs
weight: 10
---
# Chapitre 5 : Modélisation Structurelle

## Slides
{{< pdf src="/pdfs/2243.2_05_ModelisationStructurelle.pdf" >}}

## Exercices

### Exercice 1 — Bibliothèque minimale
On veut modéliser une petite application de gestion de livres d’une bibliothèque.

Voici les exigences fonctionnelles à modéliser : 
- Un livre possède un isbn (unique), un titre, et une année.
- Un auteur possède un nom et un prénom.
- Un éditeur possède un nom et une ville.
- Un livre est publié par exactement un éditeur.
- Un éditeur peut publier des livres (donc 0 ou plus).
- Un auteur peut écrire des livres (donc 0 ou plus).
- Un livre a au moins 1 auteur.

**Produire le diagramme de classes UML correspondant.**

{{< plantuml  id="Class1">}}
@startuml
hide circle
skinparam classAttributeIconSize 0

class Livre {
  +isbn: String   <<unique>>
  +titre: String
  +annee: Integer
}

class Auteur {
  +nom: String
  +prenom: String
}

class Editeur {
  +nom: String
  +ville: String
}

Editeur "1" <-- "0..*" Livre : est publié par
Auteur "0..*" <-- "1..*" Livre : est écrit par

@enduml
{{< /plantuml >}}

### Exercice 2 — Studio de capture de mouvements
Un studio réalise des sessions de capture de mouvement pour différents projets.
Chaque session utilise plusieurs appareils (caméras, IMU, microphones) et produit des clips (fichiers d'enregistrement).

Voici les exigences fonctionnelles à modéliser :
- Un projet possède un identifiant unique et un titre.
- Une session possède un identifiant unique, une date et une durée.
- Un projet peut posséder plusieurs sessions (0 ou plus).
- Une session utilise plusieurs appareils. 
- Une session produit plusieurs clips (au moins 1).
- Un appareil possède un numéro de série et une marque.
- Il existe trois types d'appareils : caméra, IMU, microphone.
- Un clip possède un identifiant unique, un fps (frames per second) et une durée.
- Un clip contient des frames (avec index, timestamp).

**Produire le diagramme de classes UML correspondant.**

{{< plantuml  id="Class2">}}
@startuml
hide circle
skinparam classAttributeIconSize 0

class Projet {
  +id: String <<unique>>
  +titre: String
}

class Session {
  +id: String <<unique>>
  +date: Date
  +duree: Integer
}

Projet *-- "0..*" Session : possède

class "Appareil {abstract}" {
  +numSérie: String
  +marque: String
}
abstract "Appareil {abstract}" 

class Camera {
}
class IMU {
}
class Microphone {
}

"Appareil {abstract}" <|-- Camera
"Appareil {abstract}" <|-- IMU
"Appareil {abstract}" <|-- Microphone

Session o-- "1..*" "Appareil {abstract}" : utilise

class Clip {
  +id: String <<unique>>
  +fps: Integer
  +duree: Integer
}

Session *-- "1..*" Clip : produit

class Frame {
  +index: Integer
  +timestamp: Float
}

Clip *-- "1..*" Frame : contient
@enduml

{{< /plantuml >}}
