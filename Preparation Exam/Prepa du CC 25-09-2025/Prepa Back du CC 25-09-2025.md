---
tags:
  - exam
  - POO
  - eng
---
## Etat de l'art 
### Petit rappel UML de classes

- `..|>` **Réalisation (implémente une interface)**  
```puml
@startuml
interface ModelListener {
  + update() : void
}
class ValueView
ValueView ..|> ModelListener
@enduml

```
    Sens : la classe de gauche **implémente** l’interface à droite (triangle côté interface).  
    Exemple : `ValueView ..|> ModelListener` (la vue implémente `ModelListener`).
    
- `o--` **Agrégation (has-a faible)**  
```puml
@startuml
class Todo
class TodoModel
TodoModel o-- Todo
@enduml

```
    Sens : **losange creux** côté agrégat : l’objet agrégateur **contient/référence** des éléments qui **peuvent vivre sans lui**.  
    Exemple : `TodoModel o-- Todo` (le modèle contient des todos, mais un `Todo` peut exister seul).
    
- `-->` **Association dirigée (référence / utilise)**  
```puml
@startuml
class Controller
class Model
Controller --> Model : uses
@enduml

```
    Sens : la classe de gauche **détient une référence** ou **utilise** celle de droite (navigation vers la droite).  
    Exemple : `Controller --> Model` (le contrôleur appelle le modèle).
### Liste des design patterns les plus utilisés

#### 1) Singleton

**Pourquoi ?** Garantir **une seule instance** (ex: config, logger).  
**Comment ?** Constructeur privé + méthode statique `getInstance()`.

**Exemple (Config appli)** : un `ConfigManager` lu une fois, utilisé partout.

```plantuml
@startuml
class ConfigManager {
  - static instance : ConfigManager
  - ConfigManager()
  + static getInstance() : ConfigManager
  + get(key : String) : String
}
@enduml
```


---

#### 2) Prototype

**Pourquoi ?** **Cloner** rapidement des objets coûteux à créer.  
**Comment ?** Interface `clone()` qui retourne une copie.

**Exemple (Document modèle)** : duplicer un modèle et modifier le titre.

```plantuml
@startuml
interface Prototype {
  + clone() : Prototype
}
class Document implements Prototype {
  - titre : String
  - contenu : String
  + clone() : Document
}
Prototype <|.. Document
@enduml
```

---

####  Abstract Factory

**Pourquoi ?** Créer des **familles** d’objets liés sans lier le code aux classes concrètes.  
**Comment ?** Une factory abstraite avec méthodes de création par type.

**Exemple (UI thème clair/sombre)** : `createButton()` et `createCheckbox()` renvoient versions Light/Dark.

```plantuml
@startuml
interface UIFactory {
  + createButton() : Button
  + createCheckbox() : Checkbox
}
interface Button
interface Checkbox

class LightFactory
class DarkFactory
class LightButton
class DarkButton
class LightCheckbox
class DarkCheckbox

UIFactory <|.. LightFactory
UIFactory <|.. DarkFactory
Button <|.. LightButton
Button <|.. DarkButton
Checkbox <|.. LightCheckbox
Checkbox <|.. DarkCheckbox
@enduml
```

---

#### 4) Adapter

**Pourquoi ?** Faire coopérer deux **interfaces incompatibles**.  
**Comment ?** Un `Adapter` implémente la **cible** et utilise l’**adaptee**.

**Exemple (Paiement)** : `PaymentProcessor.pay()` s’adapte à `LegacyPay.charge()`.

```plantuml
@startuml
interface PaymentProcessor {
  + pay(amount : float) : void
}
class LegacyPay {
  + charge(total : float) : void
}
class LegacyPayAdapter implements PaymentProcessor {
  - legacy : LegacyPay
  + pay(amount : float) : void
}
PaymentProcessor <|.. LegacyPayAdapter
LegacyPayAdapter --> LegacyPay : uses
@enduml
```

---

#### 5) Composite

**Pourquoi ?** Manipuler **feuilles** et **composites** de la même façon (arbres).  
**Comment ?** Interface commune + composite contient des enfants.

**Exemple (Système de fichiers)** : `getSize()` sur fichier ou dossier.




```mermaid
classDiagram
class FSNode {
  <<interface>>
  + getSize() int
}
class FileNode {
  - size : int
  + getSize() int
}
class DirNode {
  - children : List~FSNode~
  + add(node: FSNode) void
  + getSize() int
}
FSNode <|.. FileNode
FSNode <|.. DirNode
DirNode o-- FSNode
```

---

#### 6) Décorateur

**Pourquoi ?** **Ajouter** des fonctionnalités **à la volée** sans héritage lourd.  
**Comment ?** Un décorateur enveloppe le composant et délègue.

**Exemple (Boisson + extras)** : `cost()` augmente avec `MilkDecorator`, `WhipDecorator`.

```plantuml
@startuml
interface Beverage {
  + cost() : float
}
class Espresso implements Beverage {
  + cost() : float
}
abstract class BeverageDecorator implements Beverage {
  - inner : Beverage
  + cost() : float
}
class MilkDecorator extends BeverageDecorator
class WhipDecorator extends BeverageDecorator

Beverage <|.. Espresso
Beverage <|.. BeverageDecorator
BeverageDecorator o-- Beverage
BeverageDecorator <|-- MilkDecorator
BeverageDecorator <|-- WhipDecorator
@enduml
```

```mermaid
classDiagram
class Beverage {
  <<interface>>
  + cost() float
}
class Espresso {
  + cost() float
}
class BeverageDecorator {
  <<abstract>>
  - inner : Beverage
  + cost() float
}
class MilkDecorator
class WhipDecorator

Beverage <|.. Espresso
Beverage <|.. BeverageDecorator
BeverageDecorator o-- Beverage
BeverageDecorator <|-- MilkDecorator
BeverageDecorator <|-- WhipDecorator
```

---

#### 7) Itérateur

**Pourquoi ?** Parcourir une collection **sans exposer** sa structure.  
**Comment ?** `Iterator` avec `hasNext()/next()`.

**Exemple (Playlist)** : parcourir les chansons dans l’ordre.

```plantuml
@startuml
interface Iterator<T> {
  + hasNext() : boolean
  + next() : T
}
interface Iterable<T> {
  + createIterator() : Iterator<T>
}
class Playlist implements Iterable<Song> {
  - items : List<Song>
  + createIterator() : Iterator<Song>
}
class PlaylistIterator implements Iterator<Song> {
  - index : int
  - src : Playlist
  + hasNext() : boolean
  + next() : Song
}
Iterator <|.. PlaylistIterator
Iterable <|.. Playlist
PlaylistIterator --> Playlist
@enduml
```
---
#### 8) Observer

**Pourquoi ?** **Notifier automatiquement** plusieurs abonnés quand l’état change.  
**Comment ?** `Subject` gère `register/remove/notify`, `Observer.update()`.

**Exemple (Cours bourse)** : observateurs reçoivent les nouvelles valeurs.

```plantuml
@startuml
interface Observer {
  + update(price : float) : void
}
interface Subject {
  + register(o:Observer) : void
  + remove(o:Observer) : void
  + notifyAll() : void
}
class StockTicker implements Subject {
  - observers : List<Observer>
  - price : float
  + setPrice(p:float) : void
}
class MobileApp implements Observer {
  + update(price:float) : void
}
Subject <|.. StockTicker
Observer <|.. MobileApp
StockTicker o-- Observer
@enduml
```


---

#### 9) State

**Pourquoi ?** Faire **varier le comportement** selon l’**état interne** sans `if` partout.  
**Comment ?** `Context` délègue aux objets-états.

**Exemple (Lecteur audio)** : `Stopped`, `Playing`, `Paused`.

```plantuml
@startuml
interface PlayerState {
  + play(ctx: Player) : void
  + pause(ctx: Player) : void
  + stop(ctx: Player) : void
}
class Player {
  - state : PlayerState
  + setState(s:PlayerState) : void
  + play() : void
  + pause() : void
  + stop() : void
}
class Stopped implements PlayerState
class Playing implements PlayerState
class Paused implements PlayerState

Player --> PlayerState
PlayerState <|.. Stopped
PlayerState <|.. Playing
PlayerState <|.. Paused
@enduml
```

OK Adam — version **simple & pédagogique**, **PlantUML only**, **3 exemples**.

### MVC

- **Idée** : séparer **M**étier (Model), **V**isuel (View), **C**ontrôle (Controller).
    
- **Pourquoi** : code clair, testable, plusieurs vues sur le même modèle.
    
- **Flux** :
    
    1. L’utilisateur agit sur la **View**.
        
    2. La View appelle le **Controller**.
        
    3. Le Controller modifie le **Model**.
        
    4. Le Model notifie les **Views** (Observer).
        
    5. Les Views relisent le Model et se **mettent à jour**.
        
- **Règles d’or** : métier dans **Model**, UI dans **View**, orchestration dans **Controller**.
    

---

## Exemple 1 — Compteur (boutons + slider)

Compteur : l’utilisateur clique/glisse, la View envoie l’intention au Controller. Le Controller met à jour `value` via `model.setValue(v)`. Le Model notifie et les vues relisent puis se mettent à jour
### Classes (PlantUML)

```plantuml
@startuml
package mvc {
  class Model {
    - value : int
    + getValue() : int
    + setValue(v:int) : void
    + addListener(l:ModelListener) : void
    + removeListener(l:ModelListener) : void
  }

  interface ModelListener {
    + modelChanged(m:Model) : void
  }

  class ValueView implements ModelListener {
    - model : Model
    + modelChanged(m:Model) : void
    + render() : void
  }

  class SliderView implements ModelListener {
    - model : Model
    + modelChanged(m:Model) : void
    + bindUI() : void
  }

  class Controller {
    - model : Model
    + onInc() : void
    + onDec() : void
    + onSlide(v:int) : void
  }

  Model o-- ModelListener
  ValueView ..|> ModelListener
  SliderView ..|> ModelListener
  Controller --> Model
}
@enduml
```

### Séquence (PlantUML)


```plantuml
@startuml
actor User
participant SliderView
participant Controller
participant Model
participant ValueView

User -> SliderView : glisse(v)
SliderView -> Controller : onSlide(v)
Controller -> Model : setValue(v)
Model -> ValueView : modelChanged()
Model -> SliderView : modelChanged()
ValueView -> ValueView : relit Model + render()
SliderView -> SliderView : relit Model
@enduml
```

---

## Exemple 2 — Todo List (ajouter / cocher)

Todo List : l’utilisateur saisit ou coche/decoche, les vues appellent le Controller. Le Controller ajoute ou bascule l’item dans le `TodoModel`. Le modèle notifie et la liste se re-rend avec l’état à jour.
### Classes (PlantUML)

```plantuml
@startuml
package mvc {
  class Todo {
    - id : int
    - text : String
    - done : boolean
  }

  class TodoModel {
    - items : List<Todo>
    + add(text:String) : void
    + toggle(id:int) : void
    + getAll() : List<Todo>
    + addListener(l:ModelListener) : void
    + removeListener(l:ModelListener) : void
  }

  interface ModelListener {
    + modelChanged(m:TodoModel) : void
  }

  class ListView implements ModelListener {
    - model : TodoModel
    + modelChanged(m:TodoModel) : void
    + render() : void
  }

  class InputView {
    - controller : TodoController
    + onSubmit(text:String) : void
  }

  class TodoController {
    - model : TodoModel
    + onAdd(text:String) : void
    + onToggle(id:int) : void
  }

  TodoModel o-- ModelListener
  ListView ..|> ModelListener
  TodoController --> TodoModel
  InputView --> TodoController
}
@enduml
```

### Séquence (PlantUML)

```plantuml
@startuml
actor User
participant InputView
participant TodoController as C
participant TodoModel as M
participant ListView as V

User -> InputView : entrer "Acheter lait"
InputView -> C : onSubmit("Acheter lait")
C -> M : add("Acheter lait")
M -> V : modelChanged()
V -> V : relit M + render()
@enduml
```

---

## Exemple 3 — Lecteur Audio (play/pause/stop)

Lecteur audio : clic Play/Pause/Stop sur ButtonsView, le Controller reçoit l’action. Le Controller appelle `play/pause/stop` sur `PlayerModel` (état interne). Le modèle notifie et StatusView met à jour le statut.
### Classes (PlantUML)

```mermaid
classDiagram
%% Exemple 3 — Lecteur Audio
class PlayerModel {
  - state : String
  + play() void
  + pause() void
  + stop() void
  + addListener(l) void
  + removeListener(l) void
  + getState() String
}
class ModelListener {
  <<interface>>
  + modelChanged(m) void
}
class ButtonsView {
  - controller : PlayerController
  - model : PlayerModel
  + clickPlay() void
  + clickPause() void
  + clickStop() void
  + modelChanged(m) void
}
class StatusView {
  - model : PlayerModel
  + modelChanged(m) void
  + render() void
}
class PlayerController {
  - model : PlayerModel
  + onPlay() void
  + onPause() void
  + onStop() void
}
PlayerModel o-- ModelListener
ButtonsView ..|> ModelListener
StatusView ..|> ModelListener
PlayerController --> PlayerModel
ButtonsView --> PlayerController

```

### Séquence (PlantUML)

```plantuml
@startuml
actor User
participant ButtonsView as BV
participant PlayerController as C
participant PlayerModel as M
participant StatusView as SV

User -> BV : clickPlay()
BV -> C : onPlay()
C -> M : play()
M -> BV : modelChanged()
M -> SV : modelChanged()
SV -> SV : relit M + render()
@enduml
```
## Historique des exos

## Exercice — Modéliser une appli MVC + Observer (Java/Swing)

### Objectif

Concevoir l’architecture **MVC** d’une mini-appli : un modèle entier `value`, des vues qui l’affichent, des contrôleurs (boutons/slider) qui le modifient. Produire les **diagrammes PlantUML** à chaque étape d’affinage.

### Livrables

1. Série de **diagrammes UML (PUML)** montrant l’évolution de la modélisation (étapes 1→6).
    
2. Un **diagramme final** intégré.
    
3. Une **liste de bonnes pratiques d’extension** (sans code).
    

### Contraintes

- Séparation stricte **Model / View / Controller**.
    
- Propagation des changements via **Observer** (pas d’accès direct Vue→Vue).
    
- Pas de cycles de dépendances entre packages.
    

---

### Étape 1 — Cadrage par packages (couplage global)

But : poser les **dépendances haut niveau**.

```plantuml
@startuml
title Étape 1 — Cadrage MVC (packages)
package model
package view
package controller

view ..> model
controller ..> model
@enduml
```

---

### Étape 2 — Modèle et Observer

But : définir l’**état** et le mécanisme de **notification**.

```plantuml
@startuml
title Étape 2 — Model + Observer
package model {
  class Model {
    - value : int
    + getValue() : int
    + setValue(v:int) : void
    + addListener(l:ModelListener) : void
    + removeListener(l:ModelListener) : void
  }
  interface ModelListener {
    + modelChanged(m:Model) : void
  }
  Model "1" o-- "0..*" ModelListener : listeners
}

note right of Model
  Invariants :
  - setValue notifie après MAJ réelle
  - Pas d'exceptions dans notify
end note
@enduml
```

---

### Étape 3 — Vues textuelles

But : deux vues **passives** qui observent le modèle.

```plantuml
@startuml
title Étape 3 — Vues textuelles
package model {
  class Model
  interface ModelListener
}

package view {
  class ValueView
  class TextView
  ValueView ..|> ModelListener
  TextView  ..|> ModelListener
  ValueView o--> Model : model
  TextView  o--> Model : model
}

model.Model "1" o-- "0..*" model.ModelListener
@enduml
```

---
### Étape 4 — Contrôleurs (boutons)

But : des **contrôleurs** qui traduisent les actions UI en **MAJ du modèle**.

```plantuml
@startuml
title Step4 - Controllers
package model {
  class Model
}
package controller {
  interface ActionListener
  class Controller10
  class Controller20
  class Controller30

  Controller10 ..|> ActionListener
  Controller20 ..|> ActionListener
  Controller30 ..|> ActionListener

  Controller10 o--> Model
  Controller20 o--> Model
  Controller30 o--> Model
}
@enduml
```

---

## Étape 5 — Composition de fenêtre

But : une **fenêtre** qui compose vues et branche les contrôleurs.

```plantuml
@startuml
title Step5 - MainWindow composition
package model {
  class Model
}
package view {
  class MainWindow
  class ValueView
  class TextView
}
package controller {
  class Controller10
  class Controller20
  class Controller30
}

MainWindow *-- ValueView
MainWindow *-- TextView
MainWindow ..> Controller10
MainWindow ..> Controller20
MainWindow ..> Controller30

ValueView o--> Model
TextView  o--> Model
@enduml
```

---

## Étape 6 — Extension : Slider + Règle d’activation des boutons

But : ajouter un **slider** couplé au modèle et une **vue de boutons** désactivant le bouton = valeur courante.

```plantuml
@startuml
title Step6 - Slider and ButtonsView
package model {
  class Model
  interface ModelListener
  Model "1" o-- "0..*" ModelListener
}

package view {
  class SliderView
  class ButtonsView
  SliderView  ..|> ModelListener
  ButtonsView ..|> ModelListener
  SliderView  o--> Model
  ButtonsView o--> Model
}

package controller {
  interface ChangeListener
  class SliderController
  SliderController ..|> ChangeListener
  SliderController o--> Model
  SliderController ..> SliderView
}

note bottom of ButtonsView
Contract:
- disable 10/20/30 when value equals it
- reevaluate on each notification
end note
@enduml
```

---

## Diagramme final — Vue d’ensemble

```plantuml
@startuml
title Final - MVC + Observer overview
package model {
  class Model {
    - value : int
    + getValue() : int
    + setValue(v:int) : void
    + addListener(l:ModelListener) : void
    + removeListener(l:ModelListener) : void
  }
  interface ModelListener {
    + modelChanged(m:Model) : void
  }
  Model "1" o-- "0..*" ModelListener
}

package view {
  class MainWindow
  class ValueView
  class TextView
  class SliderView
  class ButtonsView

  ValueView   ..|> ModelListener
  TextView    ..|> ModelListener
  SliderView  ..|> ModelListener
  ButtonsView ..|> ModelListener

  MainWindow *-- ValueView
  MainWindow *-- TextView
  MainWindow *-- SliderView
  MainWindow *-- ButtonsView

  ValueView   o--> Model
  TextView    o--> Model
  SliderView  o--> Model
  ButtonsView o--> Model
}

package controller {
  interface ActionListener
  interface ChangeListener
  class Controller10
  class Controller20
  class Controller30
  class SliderController

  Controller10 ..|> ActionListener
  Controller20 ..|> ActionListener
  Controller30 ..|> ActionListener
  SliderController ..|> ChangeListener

  Controller10     o--> Model
  Controller20     o--> Model
  Controller30     o--> Model
  SliderController o--> Model
  SliderController ..> SliderView
}
@enduml

```

---

## Bonnes pratiques d’extension (sans code)

- **SOC forte** : Model sans dépendances UI ; Vues sans logique métier ; Contrôleurs minces.
    
- **Observer propre** : notifie **après** MAJ réelle ; listeners tolérants (pas d’exception).
    
- **Idempotence UI** : chaque vue vérifie l’état avant d’écrire (éviter boucles).
    
- **Variabilité** : introduire des **interfaces** pour points d’extension (ex. `Formatter`, `Validator`).
    
- **Packages stables** : `view/controller` dépendent de `model`, jamais l’inverse.
    
- **Règles UI** (ex. disable boutons) encapsulées **dans une vue dédiée** (pas dans le modèle).
    
- **Évolutivité** : ajouter un nouveau contrôleur (ex. bouton “50”) **sans modifier** le modèle ni les autres vues.
    
- **Testabilité** : logique de décision dans des classes **sans UI** (ex. stratégie d’activation).
    
- **Concurrence UI** : MAJ de vues comme **réactions** aux notifications.
    
- **Traçabilité** : snapshot PUML à chaque extension.