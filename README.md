# VISION-BOT
Suite de mon projet de fin d'études : Pilotage, Vision IA, Commandes vocales &amp; IHM

# RCXD_BOT -- Pilotage, Vision IA & Interface Web

ESP32-CAM ──► Flux vidéo ──► Vision IA (YOLO)
     │                             │
     │                             ▼
Capteurs ──► Bluetooth ◄── Pilotage / Décision
     │                             │
     ▼                             ▼
   Robot                    Interface Web (Flask)




## Structure du projet

RCXD_BOT/
│
├── README.md
│   └── Documentation générale du projet
│
├── ESP32_CAM_config/
│   └── ESP32_CAM_config.ino
│       └── Configuration et gestion du flux vidéo de l’ESP32-CAM
│
├── RC_UP/
│   └── RC_UP.ino
│       └── Firmware Arduino : commandes de déplacement avant / rotation
│
├── RC_DOWN/
│   └── RC_DOWN.ino
│       └── Firmware Arduino : commandes de déplacement arrière / arrêt
│
├── PILOT/
│   │
│   ├── main.py
│   │   └── Point d’entrée du système :
│   │       - Initialisation Bluetooth
│   │       - Lancement du serveur Flask
│   │       - Activation du streaming ESP32
│   │       - Démarrage des threads (pilotage, vision, vocal)
│   │
│   ├── config.py
│   │   └── Configuration globale :
│   │       - Ports et périphériques
│   │       - URL caméra ESP32
│   │       - Paramètres IA (YOLO, seuils)
│   │
│   ├── globals.py
│   │   └── Variables globales partagées :
│   │       - États du robot
│   │       - Données capteurs
│   │       - Logs système
│   │       - Connexion Bluetooth active
│   │
│   ├── bluetooth.py
│   │   └── Communication Bluetooth :
│   │       - Connexion série PC ↔ robot
│   │       - Envoi des commandes
│   │       - Réception des données capteurs
│   │       - Gestion des reconnexions
│   │
│   ├── pilot.py
│   │   └── Pilotage et échanges de données :
│   │       - Entrées clavier/IHM 
│   │       - Transmission des commandes robot
│   │       - Réception et parsing des données embarquées
│   │
│   ├── voice.py
│   │   └── Commandes vocales :
│   │       - Reconnaissance vocale
│   │       - Analyse sémantique
│   │       - Correction et reformulation par IA
│   │       - Génération de commandes robot
│   │
│   ├── vision.py
│   │   └── Vision artificielle :
│   │       - Réception du flux vidéo ESP32
│   │       - Détection et tracking (YOLOv8)
│   │       - Suivi automatique pan/tilt
│   │       - Analyse IA d’image
│   │
│   └── server.py
│       └── Serveur Flask :
│           - API REST
│           - Streaming vidéo MJPEG
│           - Envoi des données capteurs
│           - Logs temps réel
│           - Gestion des modes de pilotage
│
└── IHM/
    │
    ├── package.json
    │   └── Dépendances et scripts du frontend
    │
    ├── vite.config.ts
    │   └── Configuration Vite
    │
    ├── tsconfig.json
    │   └── Configuration TypeScript
    │
    └── src/
        │
        ├── main.tsx
        │   └── Point d’entrée de l’application web
        │
        ├── App.tsx
        │   └── Composant racine de l’IHM
        │
        ├── components/
        │   │
        │   ├── AccelerationGauges.tsx
        │   │   └── Affichage des données d’accélération
        │   │
        │   ├── VelocityGauge.tsx
        │   │   └── Indicateur de vitesse du robot
        │   │
        │   ├── ControlMode.tsx
        │   │   └── Sélection du mode de pilotage (manuel / vocal / auto)
        │   │
        │   ├── FPVCamera.tsx
        │   │   └── Affichage du flux caméra en temps réel
        │   │
        │   ├── YoloFeed.tsx
        │   │   └── Visualisation du tracking et détections IA
        │   │
        │   ├── Joystick.tsx
        │   │   └── Pilotage manuel du robot
        │   │
        │   ├── LocationMap.tsx
        │   │   └── Localisation et représentation spatiale
        │   │
        │   ├── SystemStatus.tsx
        │   │   └── État global du système
        │   │
        │   └── SystemLog.tsx
        │       └── Logs système en temps réel
        │
        ├── ui/
        │   └── Composants UI génériques et styles réutilisables
        │
        └── figma/
            └── Maquettes, assets graphiques et design de l’IHM


### main.py

Point d'entrée. Initialise le Bluetooth, démarre Flask, active le mode
PILOT (Stream esp32 + cmd Bt), et lance les threads.

### config.py

Configuration générale : ports, URL caméra, modèle YOLO.

### globals.py

Contient toutes les variables partagées (Bluetooth, états, capteurs,
logs...).

### bluetooth.py

Connexion Bluetooth et gestion de la liaison série.

### pilot.py

Gère le pilotage clavier et la réception des données du robot.

### server.py

Serveur Flask : streaming vidéo, API capteurs, changement de mode.

### vision.py

YOLO, tracking automatique, analyse IA.

### voice.py

Commande vocale + correction LLM.




![photo_2025-12-26_19-51-36](https://github.com/user-attachments/assets/1ce8a3fa-700d-4c2a-8075-271d88e14e2e)
