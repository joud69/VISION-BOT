#  VISION-BOT

Suite de mon projet de fin d’études : **Pilotage**, **Vision IA**, **Commandes vocales** & **Interface Homme-Machine (IHM)**.

## VISION_BOT — Pilotage, Vision IA & Interface Web
![photo_2025-12-26_19-51-36](https://github.com/user-attachments/assets/7744e864-a95e-4ae1-9808-551f49364f74)


![0114](https://github.com/user-attachments/assets/a05bc8a9-c19d-4478-a2a2-8884d9efcd59)

### Architecture générale

```text
ESP32-CAM ──► Flux vidéo ──► Vision IA (YOLO)
     │                             │
     │                             ▼
Capteurs ──► Bluetooth ◄── Pilotage / Décision
     │                             │
     ▼                             ▼
   Robot                    Interface Web (Flask)



VISION_BOT/
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
│   │       - Entrées clavier / IHM
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
        ├── main.tsx
        │   └── Point d’entrée de l’application web
        │
        ├── App.tsx
        │   └── Composant racine de l’IHM
        │
        ├── components/
        │   ├── AccelerationGauges.tsx
        │   ├── VelocityGauge.tsx
        │   ├── ControlMode.tsx
        │   ├── FPVCamera.tsx
        │   ├── YoloFeed.tsx
        │   ├── Joystick.tsx
        │   ├── LocationMap.tsx
        │   ├── SystemStatus.tsx
        │   └── SystemLog.tsx
        │
        ├── ui/
        │   └── Composants UI génériques et styles réutilisables
        │
        └── figma/
            └── Maquettes, assets graphiques et design de l’IHM




            
