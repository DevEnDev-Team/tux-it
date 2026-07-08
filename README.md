# 🐧 Tux-It : Système de Notes Synchronisées & Auto-Hébergé

Tux-It est une suite logicielle moderne, performante et axée sur la confidentialité, conçue pour vous permettre de créer, gérer et synchroniser vos notes personnelles de façon totalement autonome. Inspiré de l'écosystème Linux et de son célèbre pingouin, Tux-It vous donne le contrôle total sur vos données à travers une architecture client-serveur légère et auto-hébergeable.

---

## 📸 Captures d'Écran

*(Insérez vos captures d'écran ici pour illustrer l'interface de l'application)*

| Client Desktop (C++ / Qt6) | Application Mobile (PWA) |
| :---: | :---: |
| ![Aperçu du Client Desktop](https://raw.githubusercontent.com/DevEnDev-Team/tux-it/main/Screenshot_2026-07-07_17-43-28.png) | *[Déposez votre capture mobile ici]* |

---

## 🛠️ Architecture & Composants

Le projet est structuré en plusieurs dépôts indépendants :

1. **[tux-client](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client)** : L'application de bureau C++ / Qt6. Elle gère l'affichage des notes sous forme de fenêtres collantes (sticky notes) personnalisables. Elle intègre un script d'installation automatique (`install.sh`).
2. **[tux-server](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-server)** : Le serveur de synchronisation Go. Il stocke les notes dans une base SQLite (`postit.db`) et intègre une console d'administration sécurisée.
3. **[tux-mobile](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-mobile)** : L'application PWA mobile (HTML5/JavaScript) utilisant un Service Worker pour le support hors-ligne.

---

## ☁️ Déploiement en Production (Docker)

Le serveur Go et l'application mobile PWA sont encapsulés ensemble au sein de la même **image Docker officielle** de production (`ghcr.io/devendev-team/tux-server:latest`). L'application PWA est intégrée à l'image et est servie automatiquement à la racine (`/`).

En production, vous n'avez pas besoin de cloner l'intégralité du projet de développement. Il vous suffit de démarrer le conteneur avec la configuration suivante :

### Fichier `docker-compose.yml` de production

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
```

Pour lancer le serveur en arrière-plan :
```bash
docker compose up -d
```
*Le serveur et la PWA mobile seront immédiatement opérationnels sur le port `8282`.*

---

## 💻 Compilation & Développement Local

Pour compiler le client desktop localement ou contribuer au projet, référez-vous directement aux documentations dédiées de chaque sous-module :

* Pour compiler et installer l'application de bureau : voir le [README de tux-client](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-client/README.md).
* Pour lancer et développer sur le serveur de synchronisation : voir le [README de tux-server](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-server/README.md).
* Pour l'application mobile : voir le [README de tux-mobile](file:///home/mangoz404/Documents/Projets/Logiciels/tux-it/tux-mobile/README.md).

---

## 📄 Licence
Ce projet est open source et distribué sous licence MIT. Consultez le fichier `LICENSE` pour obtenir plus de détails.
