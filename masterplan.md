# Lucezzo LED Matrix Control System - UI/UX Requirements Specification

## 1. Functional Requirements

### 1.1 Authentication System

#### 1.1.1 User Login
- **Description**: The system shall provide secure authentication via password or biometric methods.
- **Acceptance Criteria**:
  - Users can log in using password authentication
  - Users can log in using biometric authentication if supported by device
  - Login errors are clearly displayed
  - Authentication persists between app sessions

#### 1.1.2 Session Management
- **Description**: The system shall maintain user sessions securely.
- **Acceptance Criteria**:
  - Sessions expire after appropriate timeout
  - Automatic redirection to login when session expires
  - Secure storage of authentication tokens

### 1.2 Device Management

#### 1.2.1 Device Discovery
- **Description**: The system shall allow users to discover and connect to Lightbox controllers.
- **Acceptance Criteria**:
  - Users can scan for available devices via WiFi
  - Users can select connection method (WiFi, Bluetooth, Direct Connect)
  - Connection status is clearly indicated
  - Error handling for failed connections

#### 1.2.2 Device Configuration
- **Description**: The system shall allow users to configure Lightbox controllers.
- **Acceptance Criteria**:
  - Users can name devices
  - Users can assign devices to rooms/categories
  - Users can set auto-connect preferences
  - Users can enable/disable notifications

#### 1.2.3 Device Control
- **Description**: The system shall allow users to control Lightbox controllers using standardized TSL properties.
- **Acceptance Criteria**:
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
    {
      "identifier": "power",
      "name": "Power",
      "dataType": "boolean",
      "value": false
    },
    {
      "identifier": "mode",
      "name": "Mode",
      "dataType": "enum",
      "value": "Standard",
      "specs": {
        "options": ["Standard", "Eco", "Boost", "Auto"]
      }
    },
    {
      "identifier": "active_scenario",
      "name": "Active Scenario",
      "dataType": "enum",
      "value": "None",
      "specs": {
        "options": ["None", "Ocean", "Forest", "Sunshine", "Evening", "Party"],
        "has_library": true
      }
    },
    {
      "identifier": "brightness",
      "name": "Brightness",
      "dataType": "integer",
      "value": 50,
      "specs": {"min": 0.0, "max": 100.0, "step": 1.0}
    },
    {
      "identifier": "color",
      "name": "Color",
      "dataType": "string",
      "value": "#FFFFFF"
    },
    {
      "identifier": "animation",
      "name": "Animation",
      "dataType": "enum",
      "value": "None",
      "specs": {
        "options": ["None", "Wave", "Pulse", "Sway", "Fade"]
      }
    },
    {
      "identifier": "animation_speed",
      "name": "Animation Speed",
      "dataType": "enum",
      "value": "Medium",
      "specs": {
        "options": ["Slow", "Medium", "Fast"]
      }
    }
  ]
}
```

### 1.4 Pattern/Scenario Management

#### 1.4.1 Built-in Patterns
- **Description**: The system shall provide a library of built-in lighting patterns.
- **Acceptance Criteria**:
  - Users can browse built-in patterns
  - Users can preview patterns before applying
  - Users can apply patterns to controllers
  - Pattern application is confirmed to user

#### 1.4.2 Custom Pattern Creation
- **Description**: The system shall allow users to create and save custom lighting patterns.
- **Acceptance Criteria**:
  - Users can create new patterns by adjusting properties
  - Users can name and describe patterns
  - Users can save patterns to local storage
  - Users can edit existing patterns

#### 1.4.3 Pattern Management
- **Description**: The system shall provide tools to manage saved patterns.
- **Acceptance Criteria**:
  - Users can view all saved patterns
  - Users can delete custom patterns
  - Users can edit custom patterns
  - Users can apply patterns to devices

## 2. User Interface Specifications

### 2.1 Application Structure

#### 2.1.1 Navigation Model
- The application follows a tab-based navigation model with four main sections:
  - Home: Displays connected devices and quick access controls
  - Devices: Shows all available devices with detailed filtering
  - Discover: For finding and adding new devices
  - Profile: User account management

### 2.2 Screen-by-Screen Specifications

#### 2.2.1 Splash Screen
- **Purpose**: Display app branding while initializing the application
- **Components**:
  - App logo (Lucezzo logo with white background)
  - App name in branded typography
  - Gradient background using app theme colors
- **Behavior**:
  - Displays for 2 seconds
  - Transitions automatically to Login screen

 ![image](https://github.com/user-attachments/assets/c898a22b-d03d-43c5-b379-267fd79fa3b3)



#### 2.2.2 Login Screen
- **Purpose**: Authenticate users to the system
- **Components**:
  - Welcome message
  - Login type selector (Password/Biometric)
  - Username/password fields (for password login)
  - Biometric prompt (for biometric login)
  - Login button
- **Behavior**:
  - Validates input fields
  - Displays errors inline
  - Transitions to Home screen on successful login

  ![image](https://github.com/user-attachments/assets/4d8af668-8605-4411-883a-d9f3e3d4beb0)  ![image](https://github.com/user-attachments/assets/ee5999e1-68cd-46de-8d4d-f1a254894f41)





#### 2.2.3 Home Screen
- **Purpose**: Provide overview of connected devices and quick access
- **Components**:
  - Header with device count and add device button
  - Device categories section with icons for filtering
  - Recently connected devices list with status indicators
  - Quick control toggles for power status
- **Behavior**:
  - Updates device status in real-time
  - Allows filtering by device category
  - Provides quick access to device details


<img src="https://github.com/user-attachments/assets/02fa53b9-05fa-40cf-9f01-68c220121d9e">
<br>
<img src="https://github.com/user-attachments/assets/5107c328-a2cd-40d6-be67-130ac309c25f">


#### 2.2.4 Device List Screen
- **Purpose**: Display all devices with filtering capabilities
- **Components**:
  - Filter chips for status (All, Online, Offline)
  - Search bar for finding specific devices
  - Device cards with status and quick controls
  - Device count indicator
- **Behavior**:
  - Filters update list immediately
  - Search queries filter by name, type, and room
  - Device status updates in real-time

![image](https://github.com/user-attachments/assets/e852d825-70ab-499e-be64-804b74e15a52)
<br>
![image](https://github.com/user-attachments/assets/90ff9b64-730d-47ea-bcbd-569007cef385)



#### 2.2.5 Add Device Screen
- **Purpose**: Guide users through connecting new devices
- **Components**:
  - Step indicator showing current progress
  - Connection method selection (WiFi, Bluetooth, Direct)
  - Device scanning interface
  - Device configuration form
- **Behavior**:
  - Progresses through steps sequentially
  - Validates each step before proceeding
  - Confirms successful device addition

![image](https://github.com/user-attachments/assets/44225d6a-6b6b-42b7-a223-ef6b433e9ab9)<br>![image](https://github.com/user-attachments/assets/11281d8d-4ede-490d-b416-67ac552e92d1)<br>![image](https://github.com/user-attachments/assets/216d5d56-4702-460a-8e2d-c69abf396ecb)<br>![image](https://github.com/user-attachments/assets/b8645b0d-d718-4254-a49d-8c61e0132e67)






#### 2.2.6 Device Detail Screen
- **Purpose**: Provide detailed control of specific devices
- **Components**:
  - Device header with icon, name, and power toggle
  - Information section with device metadata
  - Controls section with TSL-based property controls
  - History section showing recent activities
- **Behavior**:
  - Controls update device state in real-time
  - Error handling for failed control operations
  - Immediate UI feedback for all interactions

![image](https://github.com/user-attachments/assets/94afbc1e-a282-4762-8eab-580917356645)<br>![image](https://github.com/user-attachments/assets/c79b8ad5-6dcb-4f62-9a33-ba3b0afc42a1)



#### 2.2.7 Scenario Library Screen
- **Purpose**: Browse and manage lighting scenarios
- **Components**:
  - Tab navigation between built-in and custom scenarios
  - Scenario grid with visual previews
  - Scenario details with name and description
  - Actions for applying, editing, or deleting scenarios
- **Behavior**:
  - Preview updates when selecting different scenarios
  - Confirmation when applying scenarios
  - User-created scenarios marked distinctly

![image](https://github.com/user-attachments/assets/47a116bc-f31f-4142-b29e-49067993fc59)


#### 2.2.8 Create Scenario Screen
- **Purpose**: Create or edit custom lighting scenarios
- **Components**:
  - Scenario preview with real-time updates
  - Name and description input fields
  - Color selector with hex input
  - Property controls (brightness, animation, speed)
- **Behavior**:
  - Preview updates as changes are made
  - Validation of all input fields
  - Save/update confirmation

![image](https://github.com/user-attachments/assets/046a4228-941c-40f1-a549-357bf3c82dfb)<br>![image](https://github.com/user-attachments/assets/b38401da-05b8-4103-86dd-d25c5eb072f6)




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
- **Description**: The system includes a set of predefined patterns that cannot be modified.
- **Requirements**:
  - Minimum of 5 built-in patterns (Ocean, Forest, Sunshine, Evening, Party)
  - Each pattern includes preset values for color, brightness, animation, and speed
  - Patterns are categorized by mood/theme
  - All built-in patterns are available offline

#### 3.1.2 User-Created Patterns
- **Description**: Users can create, save, and manage their own custom patterns.
- **Requirements**:
  - Users can save unlimited custom patterns
  - Custom patterns are stored locally on device
  - Custom patterns can be modified or deleted by the user
  - Custom patterns persist across app sessions

### 3.2 Pattern Management

#### 3.2.1 Pattern Creation
- **Description**: Users can create new custom patterns from scratch or by modifying existing ones.
- **Requirements**:
  - Creation interface allows setting all controller properties
  - Real-time preview of pattern effect
  - Required fields include name and at least one property setting
  - Validation prevents saving invalid patterns

#### 3.2.2 Pattern Editing
- **Description**: Users can modify saved custom patterns.
- **Requirements**:
  - Edit interface pre-populated with current pattern settings
  - Changes can be saved or discarded
  - Confirmation required for major changes
  - Original pattern preserved until save is confirmed

#### 3.2.3 Pattern Deletion
- **Description**: Users can remove custom patterns from their library.
- **Requirements**:
  - Deletion requires confirmation
  - Deleted patterns cannot be recovered
  - Currently active pattern cannot be deleted
  - System provides feedback after successful deletion

#### 3.2.4 Pattern Application
- **Description**: Users can apply patterns to connected controllers.
- **Requirements**:
  - Pattern can be applied with a single tap
  - Application confirmation is displayed
  - Error handling for failed application
  - Applied pattern is highlighted in the interface

### 3.3 Pattern Data Structure

#### 3.3.1 Pattern Model
```json
{
  "id": "string", // Unique identifier (UUID)
  "name": "string", // User-friendly name
  "description": "string", // Optional description
  "imageUrl": "string", // Reference to preview image
  "settings": {
    "color": "string", // Hex color code
    "brightness": "integer", // 0-100 value
    "animation": "string", // Animation type
    "animation_speed": "string" // Speed setting
  },
  "isUserCreated": "boolean", // Flag for custom patterns
  "createdAt": "datetime" // Creation timestamp
}
```

#### 3.3.2 Storage Requirements
- **Local Storage**:
  - Custom patterns stored in SharedPreferences
  - JSON serialization for pattern data
  - Efficient loading and saving mechanisms
  - Error handling for storage failures

#### 3.3.3 Pattern Library Organization
- **Description**: Patterns are organized for easy browsing and selection.
- **Requirements**:
  - Tabs separate built-in from custom patterns
  - Grid layout with visual previews
  - Sort options by name, date created, and usage
  - Empty state handling for no custom patterns

