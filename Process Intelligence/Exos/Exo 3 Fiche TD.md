---
tags:
  - BPMN
  - exos
---
![[Pasted image 20251113113820.png]]

Parfait. Exo 3 — version courte, complète.

# 1) Tableau α (footprint)

![[Pasted image 20251113113944.png]]
---

# 2) Déroulé Alpha (étapes utiles)

**Succession directe (>ₗ)** extraite des traces :  
X→L, X→I, X→W ; L→K, L→S ; K→R ; S→V ; R→J ; V→J ; J→M ; I→H ; H→M ; W→T ; T→M + parallélismes (K∥S, K∥V, R∥S, R∥V).

**Causalités (`→`)** :  
X→I, X→L, X→W ; L→K, L→S ; K→R ; S→V ; R→J ; V→J ; I→H ; H→M ; W→T ; T→M ; J→M.

**Parallèles (`∥`)** :  
K∥S, K∥V, R∥S, R∥V (deux chaînes en parallèle dans la branche issue de L).

---

## Paires maximales (X,Y) (clé Alpha)

- **{X} → {I, L, W}**  (XOR après X : trois branches exclusives)
    
- {L} → {K}  et {L} → {S}  (AND après L : deux sous-branches en parallèle)
    
- {K} → {R} ; {S} → {V}
    
- {R} → {J} ; {V} → {J}  (AND-join sur J : il faut R **et** V)
    
- **{H, J, T} → {M}**  (XOR-join vers M : une seule des trois mène à M)
    
- {I} → {H} ; {W} → {T}
    

> Lecture :
> 
> - **Après X** : choix exclusif entre trois routes : (X\to I\to H\to M) **ou** (X\to W\to T\to M) **ou** (X\to L) (branche longue).
>     
> - **Après L** : **AND-split** en deux chaînes parallèles : (K\to R) et (S\to V).
>     
> - **J** attend **R** et **V** (AND-join), puis **M** termine (XOR-join depuis H/J/T).
>     

---

# 3) Réseau de Petri (structure)

**Transitions** : X, I, H, W, T, L, K, S, R, V, J, M  
**Places** (issues des paires max) :

- (p_{X,ILW}) : X→{I,L,W} (XOR-split)
    
- (p_{L,K}), (p_{L,S}) : AND-split après L
    
- (p_{K,R}), (p_{S,V})
    
- (p_{R,J}), (p_{V,J}) : deux entrées → **AND-join** sur J
    
- (p_{HJT,M}) : {H,J,T}→M (XOR-join)
    
- (p_{I,H}), (p_{W,T})
    
- source (i) avec (i→X), puits (o) avec (M→o)
    

**Arcs (résumé)** :  
(i→X); X→(p_{X,ILW})→I,L,W; L→(p_{L,K})→K; L→(p_{L,S})→S;  
K→(p_{K,R})→R; S→(p_{S,V})→V; R→(p_{R,J})→J; V→(p_{V,J})→J;  
I→(p_{I,H})→H; W→(p_{W,T})→T; H→(p_{HJT,M})→M; J→(p_{HJT,M})→M; T→(p_{HJT,M})→M; M→o.

---
