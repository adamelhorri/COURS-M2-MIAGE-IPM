---
tags:
  - front
  - exos
---
## Exo 1  : 4 Boutons cycliques avec désactivation
![[Pasted image 20250901153059.png]]

### Resolution : 
#### Automate
![[Pasted image 20250903103257.png]]
#### Tableau
![[WhatsApp Image 2025-09-01 at 15.32.18.jpeg]]
## Exo 2 : 4 boutons alternatifs avec désactivation

![[Pasted image 20250901152807.png]]
### Resolution 1
#### Automate

![[WhatsApp Image 2025-09-01 at 15.24.04 1.jpeg]]
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
#### Tableau
![[Pasted image 20250903095120.png]]
Init =/a0> E1
## Exo 3 du compteur : Raté :3
Timer avec bouton start bouton pause (je l'ai raté celui là XD)
#### Cache :
![[Pasted image 20250903111353.png]]
![[Pasted image 20250903111411.png]]
![[Pasted image 20250903111420.png]]



## Exo 4 : Compteur dans les deux sens 
### énoncé
![[42bf4209-6913-4040-8981-e00a617023af.png]]

### Automate 
 
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
## Exo 5 : Feux tricolores
### Enoncé
![[Pasted image 20250903120259.png]]
Evts : 
- CStart
- CStop
- CPanne
- tr
- to
- tv
- tpo
- tpe
`tr, to, tv` = timers rouge/orange/vert. `tpo, tpe` = timers panne ON/OFF. `CStart/CStop` = marche/arrêt. `CPanne` = bascule marche↔panne.
### Automate
```puml
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


