# 🤖 VISION-BOT

Suite de mon projet de fin d’études : **Pilotage**, **Vision IA**, **Commandes vocales** & **Interface Homme-Machine (IHM)**.

## RCXD_BOT — Pilotage, Vision IA & Interface Web

### Architecture générale

```text
ESP32-CAM ──► Flux vidéo ──► Vision IA (YOLO)
     │                             │
     │                             ▼
Capteurs ──► Bluetooth ◄── Pilotage / Décision
     │                             │
     ▼                             ▼
   Robot                    Interface Web (Flask)
