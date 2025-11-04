---
tags:
  - front
  - exam
---
[[Programmation Front]]
## Travail demandé

1. **Lecture et compréhension du code fourni**
    
    - Identifier où se trouvent les **états (`useState`)** et à quoi ils servent.
```md
"""
    { id: 1, title: "Apprendre React", status: "pending" },

    { id: 2, title: "Coder une TodoApp", status: "done" },
"""
usestate ici sert à set le getter et setter des TODOs
```
    - Expliquer comment `tasks` est passé du composant `App` vers `TaskList`.
Par import ?
2. **Ajout d’une nouvelle tâche**
    
    - Modifier `AddTaskInput` et `AddTaskButton` pour permettre d’ajouter une tâche à la liste.
        
    - Chaque nouvelle tâche doit avoir un `id` unique, un `title` et un `status` par défaut à `"pending"`.
        
3. **Suppression des tâches terminées**
    
    - Compléter `ClearButton` pour supprimer toutes les tâches ayant `status === "done"`.
        
4. **Filtrage des tâches**
    
    - Compléter `FilterDropdown` pour afficher soit :
        
        - Toutes les tâches,
            
        - Seulement celles en cours (`pending`),
            
        - Seulement celles terminées (`done`).
            
5. **Gestion du statut via la checkbox**
    
    - Compléter `TaskCheckbox` pour que cliquer dessus change le statut de la tâche (`pending` ↔ `done`).