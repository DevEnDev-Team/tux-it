# Architecture de la Stack & Squelette Minimal (C++ / Qt 6)

Ce fichier définit la structure d'un logiciel de Post-it ultra-léger pour Linux, configuré pour consommer le moins de ressources possible (cible : < 20 Mo de RAM) tout en gérant le maintien au premier plan (`Always on Top`).

## 1. Choix Technologiques & Justifications

* **Langage :** C++17 ou C++20 (Performance brute, gestion mémoire prévisible).
* **Framework UI :** Qt 6 (QtWidgets) — 
* **Système de Build :** CMake.


.
├── CMakeLists.txt
├── main.cpp
├── istorageprovider.h       # Interface SOLID (DIP / OCP)
├── localstorageprovider.h   # Implémentation de la persistance locale
├── localstorageprovider.cpp
├── notemodel.h              # Encapsulation des données de la Note (SRP)
├── stickywindow.h           # Vue Graphique (SRP)
└── stickywindow.cpp

Gestion stricte de la mémoire : Remplacement des pointeurs bruts par des pointeurs intelligents (std::unique_ptr et std::shared_ptr). La hiérarchie d'objets parents/enfants de Qt se charge de détruire les composants de l'IHM, éliminant tout risque de fuite mémoire.

Découplage IHM / Persistance : Grâce à IStorageProvider, vous pouvez implémenter à l'avenir un système d'écriture asynchrone (par exemple avec un mécanisme de Debounce ou un Worker Thread séparé) pour éviter de bloquer l'IHM lors des écritures rapides sur disque SSD, sans jamais altérer le code graphique de la note.

Poids plume (QtWidgets vs QML) : En évitant QML et son moteur de rendu par arbre de scène lourd, QtWidgets dessine l'interface directement via le moteur logiciel 2D natif du système, stabilisant l'empreinte de l'application sous le seuil critique des 15 Mo de RAM.

