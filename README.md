# 🦊 Tux-It : Vos Notes Mignonnes & Synchronisées

Bienvenue dans **Tux-It** (anciennement Post-It), une application de notes adhésives (stickies) moderne, performante et adorable pour Linux, mettant en scène notre mascotte : un petit renard espiègle.

Ce projet est entièrement open source et auto-hébergeable. Il est structuré en architecture multi-dépôts à l'aide de **sous-modules Git** :

1. **[tux-client](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client)** : Le client desktop léger écrit en **C++ (Qt6)**.
2. **[tux-server](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-server)** : Le serveur de synchronisation ultra-performant écrit en **Go (SQLite)**.

---

## 🛠️ Clonage du Projet (Sous-modules Git)

Pour récupérer ce dépôt ainsi que tous ses sous-modules associés, vous devez cloner le projet de manière récursive :

```bash
git clone --recursive https://github.com/votre-compte/tux-it.git
```

Si vous avez déjà cloné le dépôt sans les sous-modules, vous pouvez les initialiser et les mettre à jour avec :

```bash
git submodule update --init --recursive
```

---

## 🏗️ Structure du Projet

* **`tux-client/`** : Code source de l'application cliente (Qt6 C++). Vous y trouverez les scripts d'installation (`install.sh`) et de désinstallation (`uninstall.sh`).
* **`tux-server/`** : Code source du serveur Go, contenant son `Dockerfile` et sa base SQLite locale (ignorée par Git).
* **`docker-compose.yml`** : Fichier d'orchestration global situé à la racine pour déployer le serveur de synchronisation instantanément.
* **`tux-client/DESIGN.md`** : Spécifications techniques, design system et charte graphique de l'interface.
* **`STACK.md`** : Technologies et frameworks utilisés pour concevoir Tux-It.

---

## ☁️ Déploiement Rapide du Serveur (Docker Compose)

À la racine de ce dépôt, vous pouvez compiler et lancer le serveur de synchronisation Go en une commande :

1. Ouvrez le fichier [docker-compose.yml](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/docker-compose.yml) et configurez votre mot de passe d'administration (`ADMIN_PASSWORD`).
2. Lancez le service :
   ```bash
   docker compose up --build -d
   ```
*Le serveur sera accessible sur `http://localhost:8282` et la console d'administration sur `http://localhost:8282/admin`.*

---

## 💻 Compilation & Utilisation du Client

Veuillez vous référer au fichier [README.md de tux-client](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client/README.md) pour installer les dépendances Qt6 nécessaires et compiler l'application de notes.

---

## 📄 Licence
Ce projet est distribué sous licence MIT. Pour plus d'informations, consultez le fichier `LICENSE`.
