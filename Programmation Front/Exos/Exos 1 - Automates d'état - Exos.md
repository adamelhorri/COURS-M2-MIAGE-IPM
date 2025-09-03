---
tags:
  - front
  - exos
---

## Exo 1 : 4 boutons alternantifs avec désactivation

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
## Exo 2 : 4 Boutons cycliques avec desctivation
![[Pasted image 20250901153059.png]]

### Resolution : 
#### Automate
![[Pasted image 20250903103257.png]]
#### Tableau
![[WhatsApp Image 2025-09-01 at 15.32.18.jpeg]]
## Exo 3 du compteur : Raté :3

#### Cache :
![[Pasted image 20250903111353.png]]
![[Pasted image 20250903111411.png]]
![[Pasted image 20250903111420.png]]



## Exo 4 : 


