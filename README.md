# 🐧 Tux-It : Système de Notes Synchronisées & Auto-Hébergé

Tux-It est une suite logicielle moderne, performante et axée sur la confidentialité, conçue pour vous permettre de créer, gérer et synchroniser vos notes personnelles de façon totalement autonome. Inspiré de l'écosystème Linux et de son célèbre pingouin, Tux-It vous donne le contrôle total sur vos données à travers une architecture client-serveur légère et auto-hébergeable.

Le projet est composé de trois modules principaux :
1. **Un Client Desktop léger** écrit en **C++ (Qt6)** pour une intégration native et rapide sur votre bureau.
2. **Un Serveur de synchronisation** robuste écrit en **Go (SQLite)**.
3. **Une Application Web Mobile & PWA** en **HTML5/JavaScript** pour consulter et éditer vos notes en déplacement, même hors-ligne.

---

## 📸 Captures d'Écran

*(Insérez vos captures d'écran ici pour illustrer l'interface de l'application)*

| Client Desktop (C++ / Qt6) | Application Mobile (PWA) |
| :---: | :---: |
| ![Aperçu du Client Desktop](https://raw.githubusercontent.com/DevEnDev-Team/tux-it/main/Screenshot_2026-07-07_17-43-28.png) | *[Déposez votre capture mobile ici]* |

---

## 🛠️ Architecture & Composants

* **`tux-client/`** : L'application de bureau C++ / Qt6. Elle gère l'affichage des notes sous forme de fenêtres collantes (sticky notes) personnalisables. C'est elle qui régit les fenêtres ouvertes à l'écran. Fermer une note collante (via sa croix "X") l'archive simplement, tandis que la suppression définitive s'effectue depuis son tableau de bord.
* **`tux-server/`** : L'API de synchronisation en Go. Il stocke de façon sécurisée le flux de notes sous format JSON au sein d'une base SQLite légère et performante (`postit.db`). Il intègre également une console d'administration sécurisée accessible par navigateur.
* **`tux-mobile/`** : L'application PWA mobile. Grâce à un Service Worker avancé et à la persistance locale (`localStorage`), elle permet de gérer vos notes hors-ligne et de synchroniser automatiquement vos modifications dès le retour de la connexion, sans intercepter les requêtes d'API d'écriture.

---

## ☁️ Déploiement en Production (Serveur + Mobile PWA)

En production, vous n'avez pas besoin de cloner l'intégralité du projet de développement ni d'initialiser tous les sous-modules Git (comme le client desktop C++). Il vous suffit de déployer le **serveur Go** et le **client mobile**.

### 1. Structure requise sur le serveur
Pour que le serveur Go serve automatiquement l'application mobile PWA à sa racine (`/`), le dossier de l'application mobile (`tux-mobile`) doit être placé directement à la racine du répertoire de travail de `tux-server` :

```text
📂 répertoire-de-déploiement/
├── 📄 tux-server (Binaire compilé du serveur)
├── 📄 postit.db   (Base de données SQLite auto-générée)
└── 📂 tux-mobile/  (Dossier contenant l'application PWA mobile)
    ├── 📄 index.html
    ├── 📄 app.js
    └── 📄 sw-v25.js
```

### 2. Déploiement rapide via Docker Compose
Voici une configuration de production typique à l'aide de Docker. Cette configuration monte le dossier de la PWA mobile et la base de données dans le conteneur du serveur.

```yaml
version: '3.8'

services:
  tux-sync-server:
    image: ghcr.io/devendev-team/tux-server:latest
    container_name: tux-sync-server
    restart: always
    ports:
      - "8282:8282"
    environment:
      - ADMIN_PASSWORD=votre_mot_de_passe_securise
      - PORT=8282
    volumes:
      - ./data:/app/data
      - ./tux-mobile:/app/tux-mobile # Liaison du client mobile PWA
```

---

## 💻 Clonage & Développement Local (Complet)

Si vous souhaitez contribuer au projet ou compiler le client de bureau en local, vous devez cloner le dépôt de manière récursive afin de récupérer l'ensemble des modules :

```bash
git clone --recursive https://github.com/DevEnDev-Team/tux-it.git
```

Si le dépôt a déjà été récupéré sans ses sous-modules, vous pouvez les initialiser à tout moment avec la commande suivante :
```bash
git submodule update --init --recursive
```

### Compilation du client de bureau (Qt6)
Rendez-vous dans le répertoire `tux-client` et suivez les instructions de compilation présentes dans son [README.md](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client/README.md).

---

## 📄 Licence
Ce projet est open source et distribué sous licence MIT. Consultez le fichier `LICENSE` pour obtenir plus de détails.
