# Lucezzo LED Matrix Control System - UI/UX Requirements Specification

## 1. Functional Requirements

### 1.1 Authentication System

#### 1.1.1 User Login
**Description:** The system shall provide secure authentication via password or biometric methods.

**Acceptance Criteria:**
- Users can log in using password authentication
- Users can log in using biometric authentication if supported by device
- Login errors are clearly displayed
- Authentication persists between app sessions

#### 1.1.2 Session Management
**Description:** The system shall maintain user sessions securely.

**Acceptance Criteria:**
- Sessions expire after appropriate timeout
- Automatic redirection to login when session expires
- Secure storage of authentication tokens

### 1.2 Device Management

#### 1.2.1 Device Discovery
**Description:** The system shall allow users to discover and connect to Lightbox controllers.

**Acceptance Criteria:**
- Users can scan for available devices via WiFi
- Users can select connection method (WiFi, Bluetooth, Direct Connect)
- Connection status is clearly indicated
- Error handling for failed connections

#### 1.2.2 Device Configuration
**Description:** The system shall allow users to configure Lightbox controllers.

**Acceptance Criteria:**
- Users can name devices
- Users can assign devices to rooms/categories
- Users can set auto-connect preferences
- Users can enable/disable notifications

#### 1.2.3 Device Control
**Description:** The system shall allow users to control Lightbox controllers using standardized TSL properties.

**Acceptance Criteria:**
- Users can power devices on/off
- Users can adjust all supported controller parameters
- Control changes take effect within 1 second
- Current state is accurately reflected in UI

### 1.3 TSL Definitions

#### 1.3.1 Lightbox Controller TSL
```json
{
  "deviceType": "Controller",
  "properties": [
    { "identifier": "power", "name": "Power", "dataType": "boolean", "value": false },
    { "identifier": "mode", "name": "Mode", "dataType": "enum", "value": "Standard", "specs": { "options": ["Standard", "Eco", "Boost", "Auto"] } },
    { "identifier": "active_scenario", "name": "Active Scenario", "dataType": "enum", "value": "None", "specs": { "options": ["None", "Ocean", "Forest", "Sunshine", "Evening", "Party"], "has_library": true } },
    { "identifier": "brightness", "name": "Brightness", "dataType": "integer", "value": 50, "specs": { "min": 0.0, "max": 100.0, "step": 1.0 } },
    { "identifier": "color", "name": "Color", "dataType": "string", "value": "#FFFFFF" },
    { "identifier": "animation", "name": "Animation", "dataType": "enum", "value": "None", "specs": { "options": ["None", "Wave", "Pulse", "Sway", "Fade"] } },
    { "identifier": "animation_speed", "name": "Animation Speed", "dataType": "enum", "value": "Medium", "specs": { "options": ["Slow", "Medium", "Fast"] } }
  ]
}
```

## 2. User Interface Specifications

### 2.1 Application Structure

#### 2.1.1 Navigation Model
The application follows a tab-based navigation model with four main sections:
- **Home:** Displays connected devices and quick access controls
- **Devices:** Shows all available devices with detailed filtering
- **Discover:** For finding and adding new devices
- **Profile:** User account management

### 2.2 Screen-by-Screen Specifications

#### 2.2.1 Splash Screen
**Purpose:** Display app branding while initializing the application

**Components:**
- App logo (Lucezzo logo with white background)
- App name in branded typography
- Gradient background using app theme colors

**Behavior:**
- Displays for 2 seconds
- Transitions automatically to Login screen

#### 2.2.2 Login Screen
**Purpose:** Authenticate users to the system

**Components:**
- Welcome message
- Login type selector (Password/Biometric)
- Username/password fields (for password login)
- Biometric prompt (for biometric login)
- Login button

**Behavior:**
- Validates input fields
- Displays errors inline
- Transitions to Home screen on successful login

#### 2.2.3 Home Screen
**Purpose:** Provide overview of connected devices and quick access

**Components:**
- Header with device count and add device button
- Device categories section with icons for filtering
- Recently connected devices list with status indicators
- Quick control toggles for power status

**Behavior:**
- Updates device status in real-time
- Allows filtering by device category
- Provides quick access to device details

### 2.3 User Flow Diagrams

#### 2.3.1 Authentication Flow
```
Splash Screen → Login Screen → [Authentication Success] → Home Screen
                             → [Authentication Failure] → Login Screen (with error)
```

#### 2.3.2 Device Discovery Flow
```
Home Screen → Add Device Button → Add Device Screen → Select Connection Method
                                                    → Scan for Devices
                                                    → Select Device
                                                    → Configure Device
                                                    → Confirmation
                                                    → Home Screen (updated)
```

#### 2.3.3 Device Control Flow
```
Home Screen → Device Card → Device Detail Screen → Adjust Controls → [Control Success] → Updated UI State
                                                                  → [Control Failure] → Error Message
```

#### 2.3.4 Scenario Management Flow
```
Device Detail Screen → Scenario Button → Scenario Library → [Select Built-in] → Apply to Device → Confirmation
                                                         → [Create New] → Create Scenario Screen → Save → Library
                                                         → [Edit Existing] → Create Scenario Screen (populated) → Save
```

## 3. Scenario/Pattern Library Requirements

### 3.1 Pattern Sources

#### 3.1.1 Built-in Patterns
**Description:** The system includes a set of predefined patterns that cannot be modified.

**Requirements:**
- Minimum of 5 built-in patterns (Ocean, Forest, Sunshine, Evening, Party)
- Each pattern includes preset values for color, brightness, animation, and speed
- Patterns are categorized by mood/theme
- All built-in patterns are available offline

#### 3.1.2 User-Created Patterns
**Description:** Users can create, save, and manage their own custom patterns.

**Requirements:**
- Users can save unlimited custom patterns
- Custom patterns are stored locally on device
- Custom patterns can be modified or deleted by the user
- Custom patterns persist across app sessions

### 3.3 Pattern Data Structure
```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "imageUrl": "string",
  "settings": {
    "color": "string",
    "brightness": "integer",
    "animation": "string",
    "animation_speed": "string"
  },
  "isUserCreated": "boolean",
  "createdAt": "datetime"
}
```

This document outlines the functional and UI/UX requirements for the Lucezzo LED Matrix Control System.
