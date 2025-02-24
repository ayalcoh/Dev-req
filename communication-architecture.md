# LED Matrix Communication Architecture

## Table of Contents
1. [Mobile App to LED Matrix Flow](#1-mobile-app-to-led-matrix-flow)
2. [Command Flow Examples](#2-command-flow-examples)
3. [LightBox Controller Architecture](#3-lightbox-controller-architecture)
4. [Control Modes](#4-control-modes)
5. [Data Flow Paths](#5-data-flow-paths)
6. [Example Scenarios](#6-example-scenarios)
7. [Over-The-Air Updates](#7-over-the-air-updates)

## 1. Mobile App to LED Matrix Flow

### Direct Connection Methods

#### Bluetooth (Local Control)
```
Mobile App → BLE → LightBox → LED Matrix
```
- Direct commands for immediate control
- Low latency for real-time response
- Works without internet/server
- Limited range (≈10m)

#### WiFi (Local Network)
```
Mobile App → Local WiFi → LightBox → LED Matrix
```
- Local network communication
- Higher bandwidth than Bluetooth
- Works without internet/server
- Requires same network connection

### Server-Mediated Connection
```
Mobile App → Internet → Server → MQTT → LightBox → LED Matrix
```
- Remote control capability
- State synchronization across devices
- User authentication/authorization
- Analytics and logging

## 2. Command Flow Examples

### Turn On Single LED (Direct Bluetooth)
```
Mobile App 
└── BLE Command: {ledIndex: 5, state: ON, color: RED}
    └── LightBox Processes Command
        └── Updates LED Matrix via GPIO
```

### Update Pattern (Via Server)
```
Mobile App
└── HTTP Request to Server
    └── Server validates & processes
        └── MQTT Message to LightBox
            └── LightBox updates pattern
                └── LED Matrix displays pattern
```

## 3. LightBox Controller Architecture

```
┌─────────────────────────────────────────┐
│              LightBox Device            │
│                                         │
│  ┌──────────┐       ┌───────────────┐   │
│  │ WiFi     │       │ LED Matrix    │   │
│  │ Module   │       │ Control Logic │   │
│  └──────────┘       └───────────────┘   │
│        │                   │            │
│  ┌──────────┐       ┌───────────────┐   │
│  │ Bluetooth│       │ GPIO          │   │
│  │ Module   │       │ Interface     │   │
│  └──────────┘       └───────────────┘   │
│        │                   │            │
│  ┌──────────┐       ┌───────────────┐   │
│  │ MQTT     │       │ LED Matrix    │   │
│  │ Client   │       │ Hardware      │   │
│  └──────────┘       └───────────────┘   │
└─────────────────────────────────────────┘
```

## 4. Control Modes

### Local Mode
- Direct Bluetooth control
- Local WiFi control
- No internet required
- Immediate response
- Limited to local network range

### Remote Mode
- Server-mediated control
- Internet connection required
- Full feature access
- Analytics and logging
- Multiple device synchronization

### Hybrid Mode
- Automatic fallback between modes
- Seamless transition
- Local caching
- State synchronization when online

## 5. Data Flow Paths

### Direct Control Path
```
Mobile App → Bluetooth/Local WiFi → LightBox → LED Matrix
```
- Lowest latency
- No internet required
- Limited range
- Basic commands only

### Server Control Path
```
Mobile App → Internet → Server → MQTT → LightBox → LED Matrix
```
- Full feature set
- Remote access
- State synchronization
- Analytics & logging
- Authentication & authorization

### Hybrid Control Path
```
Mobile App → [Local Network ⟷ Internet] → LightBox → LED Matrix
```
- Automatic path selection
- Fallback capability
- State synchronization
- Best of both modes

## 6. Example Scenarios

### Local Control Scenario
User at home, connects directly to LightBox:
```
Mobile App (BLE) → LightBox → Immediate LED response
```

### Remote Control Scenario
User away from home, controls via internet:
```
Mobile App → Server → MQTT → LightBox → LED response
```

### Multi-Device Scenario
Multiple users controlling same LightBox:
```
Mobile App 1 ─┐
Mobile App 2 ─┼→ Server → MQTT → LightBox → LED Matrix
Mobile App 3 ─┘
```

## 7. Over-The-Air Updates

### OTA Update Flow
```
Mobile App → Server → MQTT → LightBox
   │                           │
   └─────── Progress ──────────┘
```

### Update Process
1. **Version Check**
   ```
   Mobile App → Server: Request latest version
   Server → Mobile App: Version info + metadata
   ```

2. **Update Initiation**
   ```
   Mobile App → Server: Request update
   Server → LightBox: Prepare for update
   LightBox → Server: Ready status
   ```

3. **Firmware Transfer**
   ```
   Server → LightBox: Firmware chunks
   LightBox → Server: Chunk acknowledgments
   ```

4. **Verification & Installation**
   ```
   LightBox: Verify firmware integrity
   LightBox: Install new firmware
   LightBox → Server: Installation status
   Server → Mobile App: Update complete
   ```

### OTA Message Formats

#### Version Check Request
```json
{
  "type": "version_check",
  "lightboxId": "string",
  "currentVersion": "1.0.0"
}
```

#### Update Initiation
```json
{
  "type": "update_request",
  "lightboxId": "string",
  "targetVersion": "1.1.0",
  "size": 1024000,
  "md5": "string",
  "timestamp": "ISO-8601"
}
```

#### Update Progress
```json
{
  "type": "update_progress",
  "lightboxId": "string",
  "progress": 45,
  "status": "downloading|verifying|installing",
  "timestamp": "ISO-8601"
}
```

### Safety Measures
- Firmware signature verification
- Backup of current firmware
- Rollback capability
- Progress monitoring
- Power loss recovery
- Connection loss handling

### MQTT Topics for OTA
```
lightbox/
├── {lightboxId}/
    ├── ota/
        ├── status      # Update status
        ├── progress    # Update progress
        ├── control     # Update commands
        └── data        # Firmware chunks
```

## Communication Protocols

### MQTT Topics Structure
```
lightbox/
├── {lightboxId}/
│   ├── status           # LightBox online/offline status
│   ├── matrix/
│   │   ├── state       # Current matrix state
│   │   ├── control     # Control commands
│   │   └── response    # Command responses
│   ├── config/         # LightBox configuration
│   └── system/         # System messages
├── users/{userId}/
│   ├── lightboxes/     # User's LightBoxes
│   └── preferences/    # User settings
└── admin/
    ├── broadcast/      # System-wide messages
    └── monitoring/     # System health data
```

### Message Formats

#### LightBox Status Message
```json
{
  "lightboxId": "string",
  "status": "online|offline",
  "connectionType": "wifi|bluetooth",
  "matrixInfo": {
    "rows": 10,
    "cols": 10,
    "firmware": "1.0.0"
  },
  "timestamp": "ISO-8601"
}
```

#### Control Command Message
```json
{
  "commandId": "uuid",
  "type": "single|group|all",
  "action": "setColor|setBrightness|setState",
  "payload": {
    "leds": [0, 1, 2],
    "color": {"r": 255, "g": 0, "b": 0},
    "brightness": 1.0
  },
  "timestamp": "ISO-8601"
}
```

#### Matrix State Update Message
```json
{
  "lightboxId": "string",
  "matrix": {
    "leds": [
      {
        "index": 0,
        "state": true,
        "color": {"r": 255, "g": 0, "b": 0},
        "brightness": 1.0
      }
    ]
  },
  "timestamp": "ISO-8601"
}
```
