#  VISION-BOT

Continuation of my final-year project: Navigation, AI Vision, Voice Commands, and Human–Machine Interface (HMI).


![photo_2025-12-26_19-51-36](https://github.com/user-attachments/assets/7744e864-a95e-4ae1-9808-551f49364f74)






https://github.com/user-attachments/assets/f1d9b3e5-fb03-4fcd-a5e9-efd10bf5d7b1






### General Architecture

```text
ESP32-CAM ──► Video stream ──► AI Vision (YOLO)
     │                              │
     │                              ▼
Sensors ──► Bluetooth ◄── Control / Decision
     │                              │
     ▼                              ▼
   Robot                     Web Interface (Flask)



VISION_BOT/
├── README.md
│   └── General project documentation
│
├── ESP32_CAM_config/
│   └── ESP32_CAM_config.ino
│       └── Configuration and management of the ESP32-CAM video stream
│
├── RC_UP/
│   └── RC_UP.ino
│       └── Arduino firmware: Navigation
│
├── RC_DOWN/
│   └── RC_DOWN.ino
│       └── Arduino firmware: Tracking
│
├── PILOT/
│   ├── main.py
│   │   └── System entry point:
│   │       - Bluetooth initialization
│   │       - Flask server startup
│   │       - ESP32 video streaming activation
│   │       - Thread startup (control, vision, voice)
│   │
│   ├── config.py
│   │   └── Global configuration:
│   │       - Ports and devices
│   │       - ESP32 camera URL
│   │       - AI parameters (YOLO, thresholds)
│   │
│   ├── globals.py
│   │   └── Shared global variables:
│   │       - Robot states
│   │       - Sensor data
│   │       - System logs
│   │       - Active Bluetooth connection
│   │
│   ├── bluetooth.py
│   │   └── Bluetooth communication:
│   │       - PC ↔ robot serial connection
│   │       - Command transmission
│   │       - Sensor data reception
│   │       - Reconnection handling
│   │
│   ├── pilot.py
│   │   └── Control and data exchange:
│   │       - Keyboard / HMI inputs
│   │       - Robot command transmission
│   │       - Embedded data reception and parsing
│   │
│   ├── voice.py
│   │   └── Voice commands:
│   │       - Speech recognition
│   │       - Semantic analysis
│   │       - AI-based correction and reformulation
│   │       - Robot command generation
│   │
│   ├── vision.py
│   │   └── Computer vision:
│   │       - ESP32 video stream reception
│   │       - Detection and tracking (YOLOv8)
│   │       - Automatic pan/tilt tracking
│   │       - AI-based image analysis
│   │
│   └── server.py
│       └── Flask server:
│           - REST API
│           - MJPEG video streaming
│           - Sensor data transmission
│           - Real-time logs
│           - Control mode management
│
└── IHM/
    ├── package.json
    │   └── Frontend dependencies and scripts
    │
    ├── vite.config.ts
    │   └── Vite configuration
    │
    ├── tsconfig.json
    │   └── TypeScript configuration
    │
    └── src/
        ├── main.tsx
        │   └── Web application entry point
        │
        ├── App.tsx
        │   └── Root HMI component
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
        │   └── Reusable UI components and styles
        │
        └── figma/
            └── HMI mockups, graphical assets, and UI design
