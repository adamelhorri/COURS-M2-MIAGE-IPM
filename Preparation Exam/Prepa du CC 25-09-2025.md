---
tags:
  - exos
  - front
  - exam
---
## Introduction
**Contrôle écrit (3h)** portant sur la [[Programmation Objet]] avancée et la [[Programmation Front]].  
L’épreuve évalue la **modélisation back et front** (sans intégration de données).

**Contenu pédagogique couvert :**
- **Front :**
    - Automate d’état / diagramme d’état-transition (state machine diagram)
    - Diagrammes de composants (notation spécifique du professeur)
    - Table de transition d’état (state transition table)
    - Passage à pseudo-code depuis la table
- **Back :**
    - Design patterns (modélisation)
    - Design pattern MVC
    - Diagramme de classes UML
## Programmation Front 
### Automates d'état
##### Exo 1
On dispose de 4 boutons numérotés de 1 à 4.
- Cliquer sur le bouton **n** active le bouton **n+1** et désactive le bouton **n**.
- Cliquer sur le bouton **4** active le bouton **1**.
![[Pasted image 20250916152128.png]]
###### **Automate d'état** : 
```mermaid
stateDiagram-v2
    [*] --> E1

    E1 --> E2 : CB1
    E2 --> E3 : CB2
    E3 --> E4 : CB3
    E4 --> E1 : CB4

```
##### Exo 2 
On dispose de 4 boutons numérotés de 1 à 4.
- Cliquer sur les boutons 1 et 2 active les boutons 3 et 4 et désactivent les boutons 1 et 2.
- Et vice vers ça
![[Pasted image 20250916153028.png]]
###### **Automate d'état**
```plantuml
@startuml
[*] --> E1 : /a0()

state E1
state E2
state E3
state E4
state E5
state E6

'--- Transitions 12 -> 34
E1 --> E2 : CB1 / a1()
E1 --> E3 : CB2 / a2()
E2 --> E4 : CB2 / a0()
E3 --> E4 : CB1 / a0()

'--- Transitions 34 -> 12
E4 --> E5 : CB3 / a3()
E4 --> E6 : CB4 / a4()
E5 --> E1 : CB4 / a0()
E6 --> E1 : CB3 / a0()

'--- Clics sur boutons désactivés


'--- Rebonds sur états de transition
E2 --> E2 : CB1 
E3 --> E3 : CB2 
E5 --> E5 : CB3 
E6 --> E6 : CB4
@enduml
```
#### Exo 3 - à faire
##### Exo 4
On dispose d'une fenêtre permettant de faire un compte à rebours avant et arrière, Bornés entre 0 et 20 , un bouton start et stop, et un afficheur de numero
![[Pasted image 20250916153553.png]]
###### **Automate d'état**
```plantuml
@startuml
title Compteur – FSM avec bornes (0s - 20s)

[*] --> E1

state E1 as "Idle" : Etat initial (arrété) E1
state E2 as "RunningForward" : E2
state E3 as "RunningBackward" : E3

' --- Start/Stop
E1 --> E2 : CStart
E2 --> E1 : CStop
E3 --> E1 : CStop

' --- Choix/Changement de direction
E2 --> E3 : CBWD
E3 --> E2 : CFWD

' --- Tick du timer
E2 --> E2 : timer / cpt += 1
E3 --> E3 : timer / cpt -= 1

' --- Limites
E2 --> E1 : timer / cpt  == 19
E3 --> E1 : timer / cpt =< 1 (gestion bug)

' --- Clics redondants


E1 --> E1 : timer / a0()
@enduml
```
##### Exo 5
Dans cet exercice plus complexe, on gère deux modes de fonctionnement du feu : **Marche** et **Panne**, avec possibilité de basculer entre eux.
**Événements disponibles :**
- `CStart` : démarrage (active l’état initial du mode courant).
- `CStop` : arrêt (retour à l’état _Off_ depuis n’importe quel état).
- `CPanne` : bascule entre _Marche_ et _Panne_.
- `tr`, `to`, `tv` : timers associés aux phases Rouge, Orange et Vert.
- `tpo`, `tpe` : timers associés aux états Panne (Orange allumé/éteint).

**Règles :**
- En mode **Marche**, le cycle suit _Rouge → Orange → Vert → Rouge_, avec déclenchement basé sur `tr`, `to`, `tv`.
- En mode **Panne**, le feu alterne _OrangeOn ↔ OrangeOff_ avec `tpo` et `tpe`.
- `CStop` ramène toujours à l’état _Off_.
- `CPanne` provoque un basculement immédiat vers l’état initial du mode opposé.
Un **automate d’état** doit être construit pour représenter ces comportements.
###### Automate d'état 
```plantuml
@startuml
title Feu de circulation – Start/Stop (init de mode), Stop sort de tous les états

' var: mode ∈ {Marche, Panne}; CPanne bascule le mode. Start va à l'initial du mode.
' (tick=0.1s)

[*] --> Off

'--- Sélection de mode à l'arrêt
Off --> Off : CPanne / mode = (mode="Marche"?"Panne":"Marche")

'--- Start : vers l'initial du mode courant
Off --> Marche.Rouge  : CStart [mode="Marche"]
Off --> Panne.OrangeOn: CStart [mode="Panne"]

'--- Stop : depuis TOUT état vers Off
Marche.Rouge  --> Off : CStop
Marche.Orange --> Off : CStop
Marche.Vert   --> Off : CStop
Panne.OrangeOn  --> Off : CStop
Panne.OrangeOff --> Off : CStop

'================ MODE MARCHE ================
state Marche {
  [*] --> Rouge
  state Rouge  : entry / t=0
  state Orange : entry / t=0
  state Vert   : entry / t=0

  Rouge  --> Rouge  : timer / t+=1
  Rouge  --> Orange : tr [t>=10] / t=0

  Orange --> Orange : timer / t+=1
  Orange --> Vert   : to [t>=5] / t=0

  Vert   --> Vert   : timer / t+=1
  Vert   --> Rouge  : tv [t>=20] / t=0

  ' Bascule de mode en marche : aller à l'initial du nouveau mode
  Rouge  --> Panne.OrangeOn  : CPanne / mode="Panne"
  Orange --> Panne.OrangeOn  : CPanne / mode="Panne"
  Vert   --> Panne.OrangeOn  : CPanne / mode="Panne"
}

'================ MODE PANNE =================
state Panne {
  [*] --> OrangeOn
  state OrangeOn  : entry / t=0
  state OrangeOff : entry / t=0

  OrangeOn  --> OrangeOn  : timer / t+=1
  OrangeOn  --> OrangeOff : tpo [t>=6] / t=0

  OrangeOff --> OrangeOff : timer / t+=1
  OrangeOff --> OrangeOn  : tpe [t>=4] / t=0

  ' Bascule de mode en panne : aller à l'initial du mode Marche
  OrangeOn  --> Marche.Rouge : CPanne / mode="Marche"
  OrangeOff --> Marche.Rouge : CPanne / mode="Marche"
}
@enduml
```
