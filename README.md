# LED Matrix Control System
## Product Requirements Document (PRD)

### Document Information
- **Version:** 1.1
- **Last Updated:** February 23, 2025
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
The LED Matrix Control System is a comprehensive solution enabling users to control smart LED matrices through mobile and web interfaces, with support for both local and remote control via WiFi or Bluetooth connections.

#### 1.2 Target Users
- **End Users:** Individuals with LED matrix displays
- **Administrators:** System managers who oversee multiple users and displays
- **Installers:** Technical staff who set up and configure displays

#### 1.3 Key Value Propositions
- Seamless control of LED matrices via mobile app
- Multiple connection methods (WiFi, Bluetooth)
- Real-time status monitoring and control
- Centralized management for multiple displays
- Intuitive user interface with advanced controls

### 2. System Architecture

#### 2.1 High-Level Components
- **Client Layer**
  - Mobile Application (Flutter)
  - Web Dashboard (React)
  
- **Communication Layer**
  - REST API Service (HTTP)
  - MQTT Service (Real-time Communication)
  
- **Business Layer**
  - Authentication Service
  - User Service
  - LED Control Service
  - Dashboard Service
  
- **Data Layer**
  - Database (PostgreSQL)
  - State Cache (Redis)
  
- **Hardware Layer**
  - Microcontroller
  - LED Matrix
  - MQTT Client (LightBox Integration)

  #### 2.2 Server Deployment Options
- **Local Server Mode**
  - Runs on local network
  - Direct device communication
  - Offline capability
  - Local data storage
  - Local MQTT broker
  
- **Cloud Server Mode**
  - AWS EC2 hosted
  - Remote access capability
  - Data synchronization
  - Cloud storage backup
  - Cloud MQTT broker
  
- **Hybrid Mode**
  - Local server primary operation
  - Cloud server backup
  - Automatic failover
  - Data synchronization between modes
  - Seamless mode switching

### 3. Core Features

#### 3.1 Mobile Application
- User authentication and authorization
- Individual LED control
- Group LED control
- Color selection and management
- Brightness control
- Connection management (WiFi/Bluetooth)
- Device pairing and configuration
- Offline mode support
- Real-time state synchronization

#### 3.2 Admin Dashboard
- User management (CRUD operations)
- LED matrix monitoring
- System statistics and analytics
- Power usage tracking
- User activity monitoring
- Remote matrix control
- System health monitoring
- Batch operations support

#### 3.3 LED Control
- Individual LED state management
- Color control (RGB)
- Brightness adjustment
- Group operations
- State persistence
- Real-time synchronization
- Pattern support
- Scheduled operations

#### 3.4 Sensors and I/O Integration
- **Input Sensors**
  - Motion detection sensors
  - Ambient light sensors
  - Temperature sensors
  
- **Output Controls**
  - Physical on/off switches
  - Dimmer switches
  - Emergency override switches
  - Smart home wall panels
  
- **Third-Party Integrations**
  - Smart home platforms (Home Assistant, HomeKit, Google Home)
  - Voice assistants (Alexa, Google Assistant, Siri)
  - Weather services
  - IFTTT support
  - Smart switches (Philips Hue, TP-Link, etc.)

### 4. Technical Requirements

#### 4.1 Mobile Application
- **Framework:** Flutter
- **Platforms:** iOS and Android
- **Minimum OS Versions:**
  - iOS: 13.0+
  - Android: 6.0+
- **Connectivity:** WiFi and Bluetooth support
- **Offline Capability:** Basic functionality without network
- **State Management:** Local caching and synchronization

#### 4.2 Backend Services
- **Server:** Node.js with Express
- **Database:** PostgreSQL
- **Cache:** Redis
- **Hosting:** AWS EC2
- **Message Broker:** EMQX
- **Real-time Communication:** MQTT

#### 4.3 Hardware Integration
- Support for variable matrix sizes
- Bluetooth LE support
- WiFi connectivity
- Local control capability
- Power management
- State persistence

#### 4.4 I/O and Integration Requirements
- **Sensor Communication**
  - GPIO interface support
  - I2C/SPI protocol support
  - Analog input processing
  - Digital input/output handling
  - Sensor data sampling rates
  
- **Third-Party APIs**
  - REST API endpoints for integrations
  - OAuth2 authentication support
  - Webhook support
  - Rate limiting
  - API versioning

- **Local Network Integration**
  - mDNS support for local discovery
  - UPnP support
  - Local API endpoints
  - Network failover handling
  - Local device pairing
  
### 5. User Interface

#### 5.1 Mobile Application UI
- Matrix visualization
- Color picker with presets
- Brightness controls
- Connection status indicator
- Pattern selection interface
- Schedule management
- Device configuration
- Error notifications

#### 5.2 Admin Dashboard UI
- User management interface
- System monitoring displays
- Analytics visualizations
- Remote control interface
- Configuration management
- Alert and notification system

### 6. Communication Protocol

#### 6.1 MQTT Topic Structure
```
lightbox/
├── devices/{deviceId}/
│   ├── status            # Device online/offline status
│   ├── state            # Current LED matrix state
│   ├── control          # Control commands to the device
│   ├── response         # Device responses/acknowledgments
│   └── config           # Device configuration
├── users/{userId}/
│   ├── devices/         # List of user's devices
│   └── preferences/     # User settings
└── system/
    ├── broadcast/       # System-wide messages
    └── monitoring/      # System health data
```

#### 6.2 MQTT Message Formats

##### 6.2.1 Device Status Message
```json
{
  "status": "online|offline",
  "timestamp": "ISO-8601",
  "connectionType": "wifi|bluetooth",
  "version": "1.0.0"
}
```

##### 6.2.2 LED State Message
```json
{
  "matrixSize": {
    "rows": 10,
    "cols": 10
  },
  "leds": [
    {
      "index": 0,
      "state": true,
      "color": {"r": 255, "g": 0, "b": 0},
      "brightness": 1.0
    }
  ]
}
```

##### 6.2.3 Control Command Message
```json
{
  "commandId": "uuid",
  "type": "single|group|all",
  "action": "setColor|setBrightness|setState",
  "payload": {
    "targetLeds": [0, 1, 2],
    "color": {"r": 255, "g": 0, "b": 0},
    "brightness": 1.0
  },
  "timestamp": "ISO-8601"
}
```

#### 6.3 MQTT Quality of Service (QoS)
- QoS 0: Real-time updates (LED states)
- QoS 1: Important commands and configurations
- QoS 2: Critical system operations

### 7. Security Requirements

#### 7.1 Authentication & Authorization
- JWT-based authentication
- Role-based access control
- Secure token management
- Password encryption
- Session management

#### 7.2 MQTT Security
- Username/password authentication
- JWT token validation
- ACL rules for topic access
- SSL/TLS encryption
- Client certificate support

#### 7.3 Data Security
- End-to-end encryption
- Secure MQTT communication
- Data encryption at rest
- Regular security audits
- Compliance with data protection regulations

#### 7.4 EMQX Configuration
##### Authentication
- Enable username/password authentication
- Use JWT tokens for client authentication
- Set up ACL rules based on username/client ID

##### Access Control Rules
- Users can only subscribe to their own topics:
  - Allow: "lightbox/devices/{deviceId}/#" where deviceId belongs to user
  - Allow: "lightbox/users/{userId}/#" where userId matches user
  - Allow: "lightbox/system/broadcast"

##### SSL/TLS Configuration
- Enable TLS 1.2/1.3
- Use strong cipher suites
- Implement certificate-based authentication for production

### 8. Future Enhancements

#### 8.1 Room Layout Integration
- Semi-transparent room layout layer
- Furniture and accessory placement
- Zone-based lighting control
- Time-based scheduling
- Template library
- 2D visualization

#### 8.2 Advanced Features
- Pattern creation and sharing
- Animation support
- Scene presets
- Group operation tools
- Advanced scheduling
- Energy optimization
- Multi-device synchronization

### 9. Implementation Phases

#### Phase 1: Foundation (Current)
- Basic mobile app implementation
- Essential backend services
- Core LED control functionality
- User authentication
- MQTT communication setup

#### Phase 2: Enhanced Features
- Advanced LED control
- Admin dashboard
- Real-time monitoring
- Performance optimization
- Pattern support

#### Phase 3: Advanced Integration
- Room layout integration
- Zone-based control
- Pattern library
- Advanced scheduling
- Multi-device support

#### Phase 4: Optimization & Scale
- Performance improvements
- Security enhancements
- Analytics implementation
- System scaling
- Advanced monitoring
