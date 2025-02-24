# LED Matrix Control System
## Product Requirements Document (PRD)

### Document Information
- **Version:** 2.0
- **Last Updated:** February 24, 2025
- **Status:** Draft

### Table of Contents
1. [Product Overview](#1-product-overview)
2. [System Architecture](#2-system-architecture)
3. [Core Features](#3-core-features)
4. [Technical Requirements](#4-technical-requirements)
5. [User Interface](#5-user-interface)
6. [Communication Protocol](#6-communication-protocol)
7. [Security Requirements](#7-security-requirements)
8. [Future Enhancements](#8-future-enhancements)
9. [Implementation Phases](#9-implementation-phases)

### 1. Product Overview

#### 1.1 Purpose
The LED Matrix Control System is a comprehensive solution that enables users to control LEDs matrix through a mobile application and web dashboard. The system utilizes LightBox controllers as intermediary devices that manage and control the physical LEDs matrix.

#### 1.2 Target Users
- **End Users:** Individuals controlling LEDs matrix through mobile app
- **Administrators:** System managers overseeing multiple users and LightBoxes
- **Installers:** Technical staff setting up LightBoxes and LEDs matrix

#### 1.3 Key Value Propositions
- Remote control of LEDs matrix via LightBox controllers
- Multiple connection methods to LightBox (WiFi, Bluetooth)
- Real-time status monitoring and control
- Centralized management of multiple LightBoxes
- Flexible and extensible control system

### 2. System Architecture

#### 2.1 System Components
- **User Interface Layer**
  - Mobile Application (Flutter)
  - Web Dashboard (React)
  
- **Backend Layer**
  - REST API Service (User Management, Configuration)
  - MQTT Broker (Real-time Communication)
  - Database & Cache System
  
- **LightBox Layer**
  - LightBox Controller
  - Local Processing Unit
  - LED Matrix Interface
  
- **Hardware Layer**
  - LED Matrix Arrays
  - Physical Connections
  - Power Management

#### 2.2 Component Interactions
- Mobile/Web Apps ↔ Backend: REST API for user management
- Mobile/Web Apps ↔ MQTT: Real-time control and updates
- LightBox ↔ MQTT: Command reception and state updates
- LightBox ↔ LED Matrix: Direct hardware control

#### 2.3 Server Deployment Options
- **Local Server Mode**
  - Self-hosted on local network
  - Direct LightBox communication
  - Local MQTT broker
  - Offline operation capability
  - Local database and cache
  
- **Cloud Server Mode**
  - AWS EC2 deployment
  - Remote access support
  - Cloud MQTT broker
  - Distributed database
  - High availability setup
  
- **Hybrid Mode**
  - Primary local server operation
  - Cloud server backup/failover
  - Data synchronization
  - Automatic mode switching
  - Split service architecture

### 3. Core Features

#### 3.1 Mobile Application
- User authentication and authorization
- LightBox discovery and pairing
- Individual LED control through LightBox
- Group LED control
- Color and brightness management
- Connection type selection (WiFi/Bluetooth)
- Real-time state synchronization
- Offline mode capabilities

#### 3.2 LightBox Functionality
- LED matrix state management
- Local processing of commands
- Real-time state updates
- Connection management (WiFi/Bluetooth)
- Offline operation support
- Firmware update capability
- Local cache of settings
- Direct LED matrix control

#### 3.3 Admin Dashboard
- User management
- LightBox monitoring and management
- System analytics
- Remote configuration
- Usage statistics
- Troubleshooting tools

  #### 3.4 I/O and Integration Systems
- **Sensor Integration**
  - Motion detection input
  - Ambient light sensing
  - Temperature monitoring
  - Occupancy detection
  - Environmental sensors
  
- **Physical Controls**
  - Hardware power switches
  - Manual override controls
  - Emergency shutoff
  - External dimmer integration
  - Status indicators
  
- **Third-Party Systems**
  - Home automation platforms
    * Home Assistant
    * Apple HomeKit
    * Google Home
  - Voice assistant integration
    * Amazon Alexa
    * Google Assistant
    * Siri
  - Smart switch compatibility
    * Philips Hue
    * Zigbee/Z-Wave devices
  - Custom API integration

### 4. Technical Requirements

#### 4.1 Mobile Application
- **Framework:** Flutter
- **Platforms:** iOS (13.0+) and Android (6.0+)
- **Features:**
  - Bluetooth LE support
  - WiFi configuration
  - Local state caching
  - Background operation
  - Push notifications

#### 4.2 Backend Infrastructure
- **Server:** Node.js with Express
- **Database:** PostgreSQL
- **Cache:** Redis
- **Hosting:** AWS EC2
- **Message Broker:** EMQX MQTT
- **APIs:** REST + MQTT

#### 4.3 LightBox Requirements
- WiFi connectivity
- Bluetooth LE support
- Local processing capability
- LED matrix interface
- State persistence
- Firmware update mechanism
- Error recovery
- Offline operation

**Operating System Compatibility:**
- **Client OS Support:**
  - Linux systems
  - Android devices
  - iOS devices
  - Windows systems (optional)

**Communication Support:**
- Standard networking protocols (TCP/IP)
- Bluetooth LE profiles for major OS
- Platform-specific SDKs/APIs:
  - Linux socket communication
  - Android BLE API
  - iOS Core Bluetooth

  #### 4.4 I/O and Integration Requirements
- **Hardware I/O**
  - Digital input/output handling
  - Analog sensor support
  - GPIO interface
  - I2C/SPI protocols
  - Serial communication
  
- **Integration Protocols**
  - REST API endpoints
  - Webhook support
  - OAuth2 authentication
  - WebSocket connections
  - Event streaming
  
- **Local Network**
  - mDNS discovery
  - UPnP support
  - Local API endpoints
  - Network failover
  - Device discovery

### 5. User Interface

#### 5.1 Mobile Application UI
- LightBox connection interface
- Matrix visualization
- Color selection tools
- Brightness controls
- Pattern selection
- Connection status
- Error notifications

#### 5.2 Admin Dashboard UI
- LightBox management
- User management
- System monitoring
- Analytics displays
- Configuration tools
- Alert management

### 6. Communication Protocol

#### 6.1 MQTT Topic Structure
```
lightbox/
├── {lightboxId}/
│   ├── sensors/           # Sensor data and states
│   │   ├── motion
│   │   ├── light
│   │   └── temperature
│   ├── controls/          # Physical control states
│   │   ├── switches
│   │   ├── dimmers
│   │   └── overrides
│   └── integrations/      # Third-party integration states
├── external/
│   ├── homeassistant/     # Home Assistant integration
│   ├── homekit/           # HomeKit integration
│   └── alexa/             # Alexa integration
```

#### 6.2 Message Formats

##### 6.2.1 LightBox Status
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

##### 6.2.2 Matrix Control Command
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

##### 6.2.3 Matrix State Update
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
#### 6.3 Platform-Specific Communication

**Linux Systems:**
- Socket communication (TCP/IP)
- MQTT client libraries
- D-Bus support (optional)
- Serial port communication (if needed)

**Android Devices:**
- Android BLE API
- WiFi Direct support
- Network Service Discovery
- Background Service support

**Cross-Platform Considerations:**
- Standard communication protocols
- Platform-agnostic message formats
- Error handling for each platform
- Connection management across OS

### 7. Security Requirements

#### 7.1 Authentication & Authorization
- JWT-based authentication
- Role-based access control
- Secure token management
- Device-specific authentication

#### 7.2 MQTT Security
- Client authentication
- Topic-based access control
- SSL/TLS encryption
- Device verification

#### 7.3 LightBox Security
- Secure boot
- Firmware verification
- Local storage encryption
- Secure configuration

### 8. Future Enhancements

#### 8.1 Room Layout Integration
- Virtual room mapping
- Zone-based control
- Furniture placement
- Lighting effects
- Scene management

#### 8.2 Advanced Features
- Pattern creation
- Animation support
- Multi-LightBox synchronization
- Energy optimization
- Advanced scheduling

### 9. Implementation Phases

#### Phase 1: Core Infrastructure
- Basic mobile app
- LightBox communication
- Essential controls
- User authentication

#### Phase 2: Enhanced Control
- Advanced LED control
- Pattern support
- Admin dashboard
- Monitoring system

#### Phase 3: Advanced Features
- Room layout system
- Advanced patterns
- Multi-device sync
- Analytics system

#### Phase 4: Optimization
- Performance tuning
- Security hardening
- Feature expansion
- System scaling
