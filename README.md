# 🐧 Tux-It : Système de Notes Synchronisées & Auto-Hébergé

Tux-It est une suite logicielle moderne, performante et axée sur la confidentialité, conçue pour vous permettre de créer, gérer et synchroniser vos notes de façon autonome. Inspiré de l'écosystème Linux et de son célèbre pingouin, Tux-It vous donne le contrôle total sur vos données à travers une architecture multi-composants légère et auto-hébergeable.

---

## 📸 Captures d'Écran

*(Insérez vos captures d'écran ici pour illustrer l'interface de l'application)*

| Client Desktop (C++ / Qt6) | Application Mobile (PWA) |
| :---: | :---: |
| ![Aperçu du Client Desktop](https://raw.githubusercontent.com/DevEnDev-Team/tux-it/main/Screenshot_2026-07-07_17-43-28.png) | *[Déposez votre capture mobile ici]* |

---

## 🛠️ Architecture & Composants

Le projet est structuré en plusieurs dépôts indépendants sous forme de sous-modules Git :

### 1. 💻 Client Desktop (`tux-client`)
* L'application de bureau native écrite en **C++ / Qt6**.
* Elle affiche et gère vos notes sous forme de fenêtres collantes (sticky notes) sur votre écran.
* **Documentation & Installation** : voir le [README de tux-client](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client/README.md).

### 2. ☁️ Serveur de Synchronisation (`tux-server`)
* Le backend robuste écrit en **Go** avec persistance **SQLite**.
* Il propose une console d'administration sécurisée accessible par navigateur pour gérer les clés d'API.
* **Documentation & Déploiement** : voir le [README de tux-server](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-server/README.md).

### 3. 📱 Application Mobile PWA (`tux-mobile`)
* L'interface web et mobile progressive (HTML5 / JavaScript) qui s'installe directement sur l'écran d'accueil de votre téléphone.
* Elle est servie automatiquement à la racine de votre instance de serveur de synchronisation.
* **Documentation** : voir le [README de tux-mobile](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-mobile/README.md).

---

## 💻 Clonage en Mode Développement Local (Complet)

Si vous souhaitez contribuer au projet global ou travailler localement sur l'ensemble de l'écosystème, vous devez cloner le dépôt de manière récursive afin de récupérer tous les sous-modules :

```bash
git clone --recursive https://github.com/DevEnDev-Team/tux-it.git
```

*(Si le dépôt a déjà été récupéré sans ses sous-modules, initialisez-les avec `git submodule update --init --recursive`)*.

---

## 📄 Licence
Ce projet est open source et distribué sous licence MIT. Consultez le fichier `LICENSE` pour obtenir plus de détails.
