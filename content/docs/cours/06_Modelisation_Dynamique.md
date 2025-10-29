---
title: "6 - Modélisation Dynamique"
type: docs
weight: 10
---
# Chapitre 6 : Modélisation Dynamique

## Slides
{{< pdf src="/pdfs/2243.2_06_ModelisationDynamique.pdf" >}}

## Exercices

### Exercice 1 - Gestion d’une session utilisateur dans un logiciel

Un logiciel Desktop gère la **session d’un utilisateur** à l’aide d’une machine à états finis.
Le but est de modéliser cette logique.

#### **Description du comportement à modéliser**

Lorsqu’un utilisateur lance le programme :

1. **L’application démarre** et attend que l’utilisateur saisisse ses identifiants. Il est dans l’état initial : `Non authentifié`

2. Après saisie, deux possibilités :

   * Si l’authentification réussit → passage à `Authentifié`
   * Si elle échoue → retour à `Non authentifié` (avec compteur d’essais incrémenté)

3. Après **3 échecs consécutifs**, le compte passe dans l’état `Bloqué`.

   * Seul un administrateur peut réinitialiser le compte

4. Depuis l'état `Session expirée`, l’utilisateur peut se **réauthentifier** pour revenir à `Authentifié`
   ou **quitter** l’application → état final.

#### À faire

1. **Identifier tous les états**, transitions et événements déclencheurs
2. **Modéliser le diagramme d'états en UML**
3. **Ajouter les actions associées** aux transitions

{{< plantuml  id="FSM_SessionUtilisateur">}}
@startuml
top to bottom direction

state "Non authentifié" as NonAuth
state "Authentifié" as Auth
state "Session expirée" as Expired
state "Bloqué" as Blocked

[*] --> NonAuth : lancerApplication
Expired --> [*] : fermerApplication

NonAuth --> Auth : Connexion OK\n{réinitialiserCompteurÉchec();}
NonAuth --> NonAuth : Connexion Échec [essais < 2]\n{incrémenterCompteurÉchec();}
NonAuth --> Blocked : Connexion Échec [essais >= 2]\n{incrémenterCompteurÉchec();}
Auth --> Expired : timeout
Auth --> NonAuth : Déconnexion\n{réinitialiserCompteurÉchec();}
Expired --> Auth : Réauthentifier OK\n{réinitialiserCompteurÉchec();}
Blocked --> NonAuth : Débloquer()\n{réinitialiserCompteurÉchec();}

Auth --> Auth : utiliserApplication

@enduml

{{< /plantuml >}}
