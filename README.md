# 📚 Vault Obsidian – Notes de cours M2 MIAGE IPM

Yo ✌️ ici Adam,
je partage mes notes de cours via ce repo Git.
Voilà comment les récupérer et les ouvrir avec **Obsidian**.

---

## 🔧 Ce qu’il faut installer

* **Obsidian** → [Télécharger ici](https://obsidian.md/download)
* **Git** → [Télécharger ici](https://git-scm.com/downloads)

Vérifie que Git marche avec :

```bash
git --version
```

---

## ⬇️ Récupérer les notes (premier pull)

Le premier pull se fait **dans ton terminal système** (pas dans Obsidian) :

```bash
cd ~/Documents
git clone https://github.com/adamelhorri/COURS-M2-MIAGE-IPM.git
```

---

## 📂 Ouvrir dans Obsidian

1. Lance **Obsidian**
2. Clique sur **Open folder as vault**
3. Choisis le dossier :

   ```
   COURS-M2-MIAGE-IPM
   ```

---

## ⚙️ Plugins à activer

Va dans **Settings → Community Plugins** :

* Coupe le **Safe Mode** (OFF)
* Installe :

  * **PlantUML** → pour afficher les diagrammes UML
  * **Terminal** → pour lancer Git directement depuis Obsidian

---

## 🔄 Mettre à jour les notes

* Depuis le **Terminal plugin** dans Obsidian :

  ```bash
  git pull
  ```
* Ou direct dans ton terminal système :

  ```bash
  cd ~/Documents/COURS-M2-MIAGE-IPM
  git pull
  ```

Tu veux que je te fasse aussi une **version ultra-courte** (genre 10 lignes max) pour que tes potes aient la flemme de rien lire ?
