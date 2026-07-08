# 🐧 Tux-It : Système de Notes Synchronisées & Auto-Hébergé

Tux-It est une suite logicielle moderne, performante et axée sur la confidentialité, conçue pour vous permettre de créer, gérer et synchroniser vos notes personnelles de façon totalement autonome. Inspiré de l'écosystème Linux et de son célèbre pingouin, Tux-It vous donne le contrôle total sur vos données à travers une architecture client-serveur légère et auto-hébergeable.

Le projet est composé de trois modules principaux :
1. **Un Client Desktop léger** écrit en **C++ (Qt6)** pour une intégration native et rapide sur votre bureau.
2. **Un Serveur de synchronisation** robuste écrit en **Go (SQLite)** et encapsulé dans une **image Docker officielle**.
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
* **`tux-server/`** : Le serveur de synchronisation en Go. Il stocke de façon sécurisée le flux de notes sous format JSON au sein d'une base SQLite légère et performante (`postit.db`). Il intègre également une console d'administration sécurisée accessible par navigateur.
* **`tux-mobile/`** : L'application PWA mobile. Grâce à un Service Worker avancé et à la persistance locale (`localStorage`), elle permet de gérer vos notes hors-ligne et de synchroniser automatiquement vos modifications dès le retour de la connexion, sans intercepter les requêtes d'API d'écriture.

---

## 💻 Installation & Compilation du Client Desktop (PC)

Pour utiliser le client de bureau Tux-It en local, vous devez cloner le dépôt de manière récursive afin de récupérer l'ensemble des modules :

```bash
git clone --recursive https://github.com/DevEnDev-Team/tux-it.git
```

*(Si le dépôt a déjà été récupéré sans ses sous-modules, initialisez-les avec `git submodule update --init --recursive`)*.

### Installation automatique via le script d'installation
Le projet fournit un script d'installation (`install.sh`) qui compile l'application en mode Release et l'installe sur votre système Linux.

1. **Installez les dépendances requises** pour Qt6 et CMake (sur Debian/Ubuntu/Mint) :
   ```bash
   sudo apt update
   sudo apt install build-essential cmake qt6-base-dev qt6-base-private-dev
   ```
2. **Accédez au dossier du client** :
   ```bash
   cd tux-client
   ```
3. **Rendez le script exécutable et lancez-le** :
   ```bash
   chmod +x install.sh
   ./install.sh
   ```

**Ce que fait ce script automatiquement** :
* Compile l'application en mode **Release** avec CMake et Make.
* Configure et crée les répertoires locaux utilisateurs requis (`~/.local/bin`, `~/.local/share/icons`, `~/.local/share/applications`).
* Copie le binaire optimisé `tux-it` dans `~/.local/bin/`.
* Génère et exporte l'icône de l'application dans `~/.local/share/icons/tux-it.png`.
* Installe le raccourci d'application (`tux-it.desktop`) dans le menu de votre environnement de bureau.

---

## ☁️ Déploiement en Production du Serveur (Docker)

Le serveur Go est entièrement packagé et distribué sous forme de conteneur Docker. En production, **il n'y a pas besoin de cloner l'intégralité du projet de développement**, seul le binaire du serveur (présent dans l'image Docker officielle) et le répertoire de l'application mobile (`tux-mobile`) sont nécessaires.

### 1. Préparation de la structure sur le serveur
Pour que le serveur serve automatiquement l'application mobile PWA à sa racine (`/`), le dossier de l'application mobile (`tux-mobile`) doit être monté à la racine du répertoire de travail de `tux-server` :

```text
📂 répertoire-de-déploiement/
├── 📄 docker-compose.yml
└── 📂 tux-mobile/  (Dossier contenant l'application PWA mobile)
    ├── 📄 index.html
    ├── 📄 app.js
    └── 📄 sw-v25.js
```

### 2. Lancement via Docker Compose
Utilisez le fichier `docker-compose.yml` suivant pour démarrer le serveur de synchronisation en production. L'image Docker officielle de Tux-It (`ghcr.io/devendev-team/tux-server:latest`) contient l'environnement d'exécution Go complet.

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
      - ./data:/app/data               # Persistance de la base de données (postit.db)
      - ./tux-mobile:/app/tux-mobile   # Liaison de l'application mobile PWA
```

Démarrez ensuite le conteneur en arrière-plan :
```bash
docker compose up -d
```
*Le serveur de synchronisation sera opérationnel sur le port `8282` de votre machine.*

---

## 📄 Licence
Ce projet est open source et distribué sous licence MIT. Consultez le fichier `LICENSE` pour obtenir plus de détails.
