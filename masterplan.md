# LED Matrix Control System - Detailed UI/UX Specifications

## 1. User Interface Architecture

### 1.1 Mobile Application (Flutter)

- **Splash Screen**: Company logo with subtle LED animation effect
- **Authentication Flow**: Login, registration, password recovery screens
- **Main Navigation**: Bottom tab navigation with 5 main sections
- **Home Dashboard**: Overview of connected LightBox with status and quick controls
- **LED Control Screen**: Interactive matrix visualization with control panels
- **Patterns Library**: Browse, apply, create, and manage lighting patterns
- **Schedule Manager**: Create and manage time-based lighting changes
- **Sensors Dashboard**: Monitor and configure connected sensors
- **Automation Rules**: Create and manage sensor-triggered lighting behaviors
- **Settings**: LightBox configuration and user profile management

## 2. Detailed Screen Specifications

### 2.1 Authentication Screens

#### 2.1.1 Login Screen
- Email field with validation
- Password field with show/hide toggle
- "Remember me" checkbox
- Primary CTA: "Log In" button (full width)
- Secondary links: "Forgot password?" and "Create account"
- Error handling for invalid credentials
- Loading state during authentication

#### 2.1.2 Registration Screen
- Name field
- Email field with validation
- Password field with strength indicator
- Confirm password field
- Terms of service checkbox with link to terms
- Primary CTA: "Create Account" button (full width)
- Secondary link: "Already have an account?"
- Step-by-step progress indicator
- Error handling for each field

#### 2.1.3 Password Recovery
- Email input screen
- Verification code input screen
- New password creation screen
- Success confirmation screen
- Clear progress indicator between steps

### 2.2 Home Dashboard

#### 2.2.1 LightBox Overview
- LightBox card with:
  - Device name (editable on long press)
  - Status indicator (online/offline)
  - Connection type icon (WiFi/Bluetooth)
  - Battery level (if applicable)
  - Quick action buttons: power toggle, brightness preset, favorite pattern
  - Thumbnail preview of current LED state
- Pull-to-refresh functionality
- Add device button (if no devices connected)

#### 2.2.2 Notifications Panel
- Accessible via bell icon in app bar
- Categorized notifications:
  - System alerts (high priority)
  - Firmware updates (medium priority)
  - Connection status changes (low priority)
- Clear all button
- Individual dismissible notifications
- Read/unread status indicators
- Timestamp for each notification

### 2.3 LightBox Discovery and Connection

#### 2.3.1 Discovery Screen
- Animated scanning visualization
- Segmented list of discovered devices:
  - Previously connected devices
  - New devices
- For each device:
  - Device name/ID
  - Signal strength indicator
  - Connection type icon
  - "Connect" button
- Manual connection option (via device ID)
- Connection type toggle (WiFi/Bluetooth)
- Refresh button
- Troubleshooting tips expandable section

#### 2.3.2 Connection Setup
- Step-by-step process with progress indicator
- For WiFi connection:
  - Available networks list
  - Password input
  - Connection security information
- For Bluetooth connection:
  - Pairing process visualization
  - PIN input if required
- Connection progress indicator with status messages
- Success confirmation with animation
- Troubleshooting options for failed connections
- "Next" button to proceed to LED control

### 2.4 LED Control Screen

#### 2.4.1 Matrix Visualization
- Interactive grid representation of LED matrix
- Dynamically sized based on LightBox configuration
- Color-accurate LED state representation
- Selection modes:
  - Single LED selection
  - Multi-select via tap and drag
  - Pattern-based selection (line, rectangle, circle)
  - "Select all" option
- Zoom controls:
  - Pinch to zoom gesture
  - Zoom in/out buttons
  - "Fit to screen" button
- Pan functionality with inertial scrolling
- Grid overlay with coordinates
- Selection highlighting with semi-transparent overlay

#### 2.4.2 Color Controls
- Color selection panel with:
  - Color wheel with brightness/saturation controls
  - RGB sliders with numerical input
  - Hex color input field
  - Eyedropper tool for sampling colors
  - Swatches of recently used colors (8 slots)
  - Saved favorite colors (long press to save)
- Brightness control:
  - Vertical slider (0-100%)
  - Preset buttons (25%, 50%, 75%, 100%)
  - Numerical input field
- Effects panel:
  - Blink effect with frequency control
  - Fade effect with duration control
  - Rainbow cycle with speed control
  - Custom effect selection

#### 2.4.3 Control Panel
- Primary action buttons:
  - "Apply" button (updates selected LEDs)
  - "All On/Off" toggle
  - "Reset to Default" button
  - "Save as Pattern" button
- Secondary controls:
  - "Undo" button (with counter)
  - "Redo" button
  - "Copy" and "Paste" for LED selections
  - "Invert Selection" button
- Mode toggles:
  - "Draw" mode
  - "Erase" mode
  - "Select" mode
  - "Pattern" mode

#### 2.4.4 LED Details Dialog
- Appears on long press of individual LED
- Shows:
  - LED coordinates/index
  - Current color (HEX and RGB values)
  - Current brightness percentage
  - On/off status
- Individual controls:
  - Color picker
  - Brightness slider
  - On/off toggle
- "Apply to selection" button
- "Copy settings" button
- Close button

### 2.5 Patterns Library

#### 2.5.1 Pattern Browser
- Segmented navigation:
  - "All Patterns"
  - "My Patterns"
  - "Favorites"
  - "Recent"
- Grid layout of pattern thumbnails:
  - 2 columns (portrait)
  - 4 columns (landscape)
- For each pattern:
  - Animated thumbnail
  - Pattern name
  - Favorite indicator (star icon)
- Sort options:
  - Newest first
  - Alphabetical
  - Most used
- Filter options:
  - By category (static, animated, etc.)
  - By color scheme
- Search bar with instant results
- "Create New" FAB

#### 2.5.2 Pattern Details
- Pattern preview:
  - Large animated visualization
  - Play/pause button for animations
  - Speed control for animations
- Information panel:
  - Pattern name
  - Creation date
  - Last modified date
  - Used count and frequency
- Action buttons:
  - "Apply to LightBox" (primary CTA)
  - "Edit Pattern"
  - "Add to Favorites"
  - "Share" (future feature)
  - "Delete" (with confirmation)
- Related patterns section

#### 2.5.3 Pattern Creator
- Matrix editor with same controls as LED Control Screen
- Animation timeline:
  - Frame-by-frame editor
  - Add/delete frames
  - Duration control for each frame
  - Copy/paste frames
  - Preview animation
- Effect builder:
  - Transition type selection
  - Speed/duration controls
  - Direction controls
  - Preview window
- Save dialog:
  - Pattern name input
  - Optional description
  - Category selection
  - Thumbnail preview
  - Private/shared toggle (future)
- Test functionality:
  - "Test on LightBox" button
  - Preview window
  - Speed adjustment

### 2.6 Schedule Manager

#### 2.6.1 Schedules List
- Calendar view toggle:
  - Day view
  - Week view
  - Month view
- Timeline view toggle:
  - Horizontal timeline
  - List view
- For each scheduled event:
  - Time range visualization
  - Pattern thumbnail
  - Event name
  - Recurrence indicator
  - Enabled/disabled toggle
- "Add Schedule" FAB
- Filter options:
  - By LightBox
  - By pattern
  - By time of day

#### 2.6.2 Schedule Creator/Editor
- Basic information:
  - Schedule name
  - Pattern selection (with preview)
  - LightBox selection
- Time settings:
  - Start time picker
  - End time picker
  - Duration visualization
- Recurrence settings:
  - One-time / Recurring toggle
  - Day selection for weekly recurrence
  - Monthly options
  - End date or repeat count
- Transition settings:
  - Fade in duration
  - Fade out duration
- Notification toggle
- Save/Cancel buttons
- "Delete Schedule" option (for existing schedules)

### 2.7 Room Layout Editor (Future Phase)

#### 2.7.1 Room Scanner
- Camera view with AR overlay
- Guide markers for optimal scanning
- Real-time 3D mesh visualization
- Progress indicator
- "Capture" button
- Guidance instructions
- Review screen:
  - 3D preview of captured space
  - Edit options
  - "Use this scan" button
  - "Scan again" button

#### 2.7.2 Layout Editor
- Top-down view of room layout
- Pan and zoom controls
- Object toolbar:
  - Walls
  - Doors
  - Windows
  - Furniture categories
  - Decorative elements
- Properties panel for selected objects:
  - Size controls
  - Orientation controls
  - Color/material selection
  - Delete button
- "Add LED Matrix" placement tool
- Layer controls:
  - Room layout layer toggle
  - LED matrix layer toggle
  - Control layer toggle
- "Save Layout" button
- "Import Floor Plan" option

#### 2.7.3 Lighting Visualization
- Combined view of room layout and LED effects
- Lighting simulation with:
  - Light spread visualization
  - Shadow effects
  - Brightness adjustment based on distance
  - Surface reflection simulation
- Time slider for animated patterns
- "Apply to LightBox" button
- "Edit Pattern" button
- "Adjust Layout" button

### 2.8 Settings Screens

#### 2.8.1 User Settings
- Profile section:
  - Profile picture (editable)
  - Name (editable)
  - Email (editable with verification)
  - Account creation date
- Preferences section:
  - Notification toggles by category
  - Theme selection (light/dark/system)
  - Language selection
  - Temperature unit (°C/°F)
- Security section:
  - Change password
  - Two-factor authentication toggle
  - Connected devices list
- Data Management:
  - Sync settings
  - Cloud storage usage
  - Clear cache option
- "Logout" button
- "Delete Account" option (with confirmation)

#### 2.8.2 LightBox Settings
- Device information:
  - Device name (editable)
  - Model number
  - Serial number
  - MAC address
  - IP address (if on WiFi)
  - Firmware version
- Connection settings:
  - Connection type preference
  - WiFi network selection
  - Bluetooth settings
- LED matrix configuration:
  - Matrix size settings
  - LED type selection
  - Default brightness
  - Power-on behavior
- Firmware section:
  - Current version information
  - Check for updates button
  - Update history
  - Auto-update toggle
- Maintenance:
  - Restart device option
  - Factory reset option
  - Diagnostic tests
- "Remove Device" option (with confirmation)

### 2.9 Sensor Management Screens

#### 2.9.1 Sensors Dashboard
- Main sensors overview with:
  - Card-based layout showing sensor categories
  - Status indicators for each sensor type (active, inactive, error)
  - Quick-view of latest readings with timestamp
  - Color-coded alerts for out-of-range values
  - Pull-to-refresh functionality
  - "Add Sensor" button
- Filter controls:
  - By sensor type (motion, environmental, acoustic, security)
  - By status (all, active, inactive, alerts)
  - By location/room
- Sorting options:
  - Most recent activity
  - Alert priority
  - Alphabetical
  - Custom order
- Batch actions menu:
  - Enable/disable multiple sensors
  - Reset calibration
  - Update firmware
  - Assign to room/zone

#### 2.9.2 Sensor Details Screen
- Header with:
  - Sensor name (editable)
  - Sensor type icon
  - Status indicator (online/offline/error)
  - Battery level (if applicable)
  - Signal strength (if wireless)
- Primary reading visualization:
  - Large numerical display for primary value
  - Appropriate visualization (gauge, indicator, graph)
  - Unit of measurement
  - Timestamp of last update
- Historical data graph:
  - Time-series chart of readings
  - Time range selector (1h, 24h, 7d, 30d)
  - Min/max indicators
  - Trend line
  - Export data option
- Secondary readings section:
  - Additional data points from multi-function sensors
  - Mini visualizations for each data point
- Configuration panel:
  - Sensitivity slider/input
  - Threshold settings
  - Update frequency
  - Calibration controls
  - Advanced settings expandable section
- Location assignment:
  - Room/zone dropdown
  - "Locate on Floor Plan" button
- Associated automations list:
  - Rules using this sensor as trigger
  - Toggle to enable/disable per rule
  - "Add Rule" button
- Maintenance section:
  - Firmware version and update button
  - Reset to defaults
  - Diagnostic test button
  - Removal process

#### 2.9.3 Add Sensor Screen
- Sensor discovery section:
  - Animated scanning visualization
  - List of discovered sensors with:
    - Sensor ID/name
    - Type detection
    - Signal strength
    - "Connect" button
- Manual addition section:
  - Sensor type selection
  - ID/serial input
  - Connection method options
  - "Add Manually" button
- Setup wizard with:
  - Step-by-step progress indicator
  - Connection status feedback
  - Location assignment
  - Naming step
  - Initial calibration
  - Testing confirmation
- Success confirmation with:
  - Animated checkmark
  - Sensor details summary
  - "Configure Now" or "Done" buttons

### 2.10 Automation Rules Screens

#### 2.10.1 Rules List
- Segmented navigation:
  - "Active Rules"
  - "Inactive Rules"
  - "Templates"
- For each rule:
  - Rule name
  - Brief condition summary
  - Brief action summary
  - Enabled/disabled toggle
  - Status indicator (active/waiting/error)
- Sorting options:
  - Recently triggered
  - Alphabetical
  - Custom order
- Filtering options:
  - By sensor type
  - By action type
  - By location
- "Create Rule" FAB
- Batch actions menu:
  - Enable/disable selection
  - Duplicate
  - Delete

#### 2.10.2 Rule Creation/Editor
- Rule name input
- Trigger section:
  - "When" statement builder
  - Sensor selection with search
  - Condition options (specific to sensor type)
  - Value thresholds with sliders/inputs
  - Time condition options
  - Multiple condition support (AND/OR logic)
  - Condition preview in natural language
- Action section:
  - "Then" statement builder
  - Action type selection (change LEDs, activate pattern, etc.)
  - Target LightBox selection
  - Action parameters (specific to action type)
  - Transition settings (fade time, delay)
  - Multiple action sequence support
  - Action preview visualization
- Advanced options:
  - Repeat behavior settings
  - Cooldown period
  - Priority level
  - Notification settings
- Test functionality:
  - "Test Rule" button
  - Real-time feedback
  - Success/failure indication
- Save/cancel buttons
- "Delete Rule" option (for existing rules)

#### 2.10.3 Rule Templates
- Grid of pre-defined rule templates:
  - Motion-activated lighting
  - Occupancy timeout
  - Environmental response
  - Sound-reactive effects
  - Security alerts
- For each template:
  - Illustrative icon
  - Template name
  - Brief description
  - Complexity indicator
  - "Use Template" button
- Customization view:
  - Pre-filled rule editor
  - Highlighted customization points
  - Guide text for adaptations
  - "Save as Custom Rule" button

## 3. User Flows

### 3.1 First-Time User Experience

1. User installs and opens app
2. Splash screen displayed briefly
3. Onboarding screens introduce key features (3-4 screens)
4. Registration/Login screen presented
5. After authentication, LightBox discovery screen appears
6. User follows guided process to connect first LightBox
7. Quick tutorial overlay highlights main controls
8. User completes first action (turn on LED, change color)
9. Success celebration animation
10. User directed to Home Dashboard

### 3.2 LED Control Flow

1. User selects a LightBox from dashboard
2. LED Control screen loads with current matrix state
3. User selects LEDs (single tap, multi-select, or pattern select)
4. User chooses color and brightness
5. User taps "Apply" to update selected LEDs
6. Real-time confirmation as LEDs update
7. User can continue editing or save as pattern
8. When finished, user returns to dashboard or navigates to another section

### 3.3 Pattern Creation Flow

1. User navigates to Pattern Library
2. User taps "Create New" button
3. Pattern Creator opens with blank matrix or current state
4. User designs initial LED state
5. For static pattern:
   - User finalizes design
   - User taps "Save Pattern"
   - User enters name and details
   - User returns to Pattern Library
6. For animated pattern:
   - User taps "Add Frame"
   - User designs next frame
   - User sets timing
   - User repeats until animation complete
   - User previews animation
   - User saves with name and details

### 3.4 Schedule Creation Flow

1. User navigates to Schedule Manager
2. User taps "Add Schedule" button
3. Schedule Creator opens
4. User enters schedule name
5. User selects pattern from library
6. User sets time parameters and recurrence
7. User selects target LightBox
8. User saves schedule
9. New schedule appears in list
10. At scheduled time, app sends notification (if enabled)
11. Pattern automatically applies to LightBox

### 3.5 Room Layout Integration Flow

1. User navigates to Room Layout section
2. For new layout:
   - User chooses creation method (scan, draw, import)
   - User follows method-specific process
   - Basic layout is created
3. User adds/adjusts furniture and objects
4. User places LED matrix in layout
5. User switches to lighting visualization mode
6. User tests different patterns in room context
7. User saves layout with name
8. User can apply visualized pattern to actual LightBox

### 3.6 Sensor Integration Flow

1. User navigates to Sensors Dashboard
2. User taps "Add Sensor" button
3. Discovery screen scans for available sensors
4. User selects sensor from discovered list or adds manually
5. Step-by-step setup guides through connection process
6. User assigns sensor to a room/location
7. User names the sensor and configures basic settings
8. Initial calibration process runs if needed
9. Success confirmation shows sensor is ready
10. User is returned to updated Sensors Dashboard

### 3.7 Automation Rule Creation Flow

1. User navigates to Automation Rules screen
2. User taps "Create Rule" button
3. User enters rule name
4. User builds trigger condition:
   - Selects sensor from list
   - Configures condition parameters
   - Adds any time constraints
   - Adds additional conditions if needed
5. User builds action sequence:
   - Selects action type
   - Chooses target devices
   - Configures specific parameters
   - Adds transitions or delays
   - Adds additional actions if needed
6. User configures advanced options
7. User tests rule functionality
8. User saves rule
9. New rule appears in rules list
10. System begins monitoring for trigger conditions

## 4. Interaction Specifications

### 4.1 LED Matrix Interactions

- **Tap**: Select single LED or toggle selection in multi-select mode
- **Double Tap**: Reset view to show entire matrix
- **Long Press**: Open detailed control for specific LED
- **Tap and Drag**: Select multiple LEDs in a line or region
- **Swipe**: Pan across matrix when zoomed in
- **Pinch**: Zoom in/out of matrix view
- **Two-finger Rotate**: Rotate view (if supported by matrix)

### 4.2 Color Selection Interactions

- **Tap Color Wheel**: Select color at tap point
- **Drag on Color Wheel**: Fine-tune color selection
- **Tap Slider**: Jump to position
- **Drag Slider**: Smooth adjustment
- **Tap Swatch**: Apply saved color
- **Long Press Swatch**: Save current color to swatch
- **Double Tap RGB Field**: Open numerical input keyboard

### 4.3 Pattern Library Interactions

- **Tap Pattern**: Open pattern details
- **Long Press Pattern**: Show quick action menu (apply, edit, favorite)
- **Swipe Pattern Left**: Quick delete (with confirmation)
- **Swipe Pattern Right**: Quick favorite toggle

### 4.4 Schedule Interactions

- **Tap Schedule**: Open schedule details
- **Tap Toggle**: Enable/disable schedule
- **Swipe Schedule Left**: Quick delete (with confirmation)
- **Drag on Timeline**: Adjust schedule duration

### 4.5 Room Layout Interactions

- **Tap Object**: Select object in layout
- **Drag Object**: Move object in layout
- **Pinch Object**: Resize object
- **Two-finger Rotate**: Rotate object
- **Double Tap Object**: Open object properties
- **Tap and Hold Empty Space**: Add new object menu

### 4.6 Gesture Consistency Rules

- Long press always reveals detailed options
- Swipe left/right for destructive/constructive quick actions
- Double tap for reset or default views
- Tap and drag for selection or movement
- Two-finger gestures for view manipulation

### 4.7 Sensor Interaction Patterns

- **Tap Sensor Card**: Open detailed sensor view
- **Long Press Sensor Card**: Show quick action menu
- **Swipe Sensor Card Left**: Quick disable
- **Swipe Sensor Card Right**: Quick recalibrate
- **Pull Down**: Refresh sensor data
- **Tap Graph**: Show specific data point values
- **Pinch Graph**: Zoom time scale
- **Two-finger Drag Graph**: Pan through time periods
- **Tap Settings Icon**: Open sensor configuration
- **Tap Alert Icon**: Show alert details and resolution options

### 4.8 Automation Rule Interactions

- **Tap Rule**: Open rule details/editor
- **Tap Toggle**: Enable/disable rule
- **Swipe Rule Left**: Delete rule (with confirmation)
- **Long Press Rule**: Show quick action menu
- **Drag Handle**: Reorder rules (priority)
- **Tap Condition Block**: Expand/edit condition
- **Tap Action Block**: Expand/edit action
- **Tap + Button**: Add condition or action
- **Drag Between Blocks**: Reorder actions in sequence

## 5. Visual Design Guidelines

### 5.1 Color Palette

- **Primary Color**: #2D7CEB (Blue)
- **Secondary Color**: #FF5722 (Orange)
- **Background Colors**:
  - Light theme: #FFFFFF (White), #F5F7FA (Light Gray)
  - Dark theme: #121212 (Black), #1E1E1E (Dark Gray)
- **Accent Colors**:
  - Success: #4CAF50 (Green)
  - Warning: #FFC107 (Amber)
  - Error: #F44336 (Red)
  - Info: #2196F3 (Light Blue)
- **Text Colors**:
  - Primary text: #212121 (Dark Gray)
  - Secondary text: #757575 (Medium Gray)
  - Disabled text: #9E9E9E (Light Gray)
  - Light theme contrast text: #FFFFFF (White)
- **Sensor Status Colors**:
  - Normal: #4CAF50 (Green)
  - Warning: #FF9800 (Orange)
  - Critical: #F44336 (Red)
  - Inactive: #9E9E9E (Gray)
  - Calibrating: #8C9EFF (Light Purple)

### 5.2 Typography

- **Primary Font**: Roboto
- **Headings**:
  - H1: Roboto Medium, 24sp
  - H2: Roboto Medium, 20sp
  - H3: Roboto Medium, 18sp
  - H4: Roboto Medium, 16sp
- **Body Text**:
  - Body 1: Roboto Regular, 16sp
  - Body 2: Roboto Regular, 14sp
- **Small Text**:
  - Caption: Roboto Light, 12sp
  - Overline: Roboto Medium, 10sp, all caps
- **Buttons**:
  - Primary: Roboto Medium, 16sp
  - Secondary: Roboto Medium, 14sp

### 5.3 Component Styles

#### 5.3.1 Buttons
- **Primary Button**:
  - Background: Primary color
  - Text: White
  - Elevation: 2dp
  - Corner radius: 8dp
  - Height: 48dp
  - Horizontal padding: 16dp
- **Secondary Button**:
  - Border: 1.5dp Primary color
  - Text: Primary color
  - Elevation: 0dp
  - Corner radius: 8dp
  - Height: 48dp
  - Horizontal padding: 16dp
- **Icon Button**:
  - Size: 40dp x 40dp
  - Touch target: 48dp x 48dp
  - Ripple effect on tap

#### 5.3.2 Cards
- **Standard Card**:
  - Background: Surface color
  - Elevation: 1dp
  - Corner radius: 12dp
  - Padding: 16dp
- **LightBox Card**:
  - Background: Surface color
  - Elevation: 2dp
  - Corner radius: 12dp
  - Padding: 16dp
  - Image height: 120dp
  - Title size: H3
  - Subtitle size: Body 2

#### 5.3.3 Input Fields
- **Text Field**:
  - Background: Light Gray (Light theme), Dark Gray (Dark theme)
  - Border: None (flat) or 1dp line
  - Corner radius: 8dp
  - Height: 56dp
  - Label: Caption size, above field
  - Helper text: Caption size, below field
  - Error state: Red border and text
- **Checkbox**:
  - Size: 24dp x 24dp
  - Touch target: 48dp x 48dp
  - Label: Body 2 size

#### 5.3.4 Tabs
- **Navigation Tabs**:
  - Height: 56dp
  - Icon size: 24dp
  - Label: Caption size
  - Active indicator: 2dp line or pill shape
  - Active color: Primary color
  - Inactive color: Gray

### 5.4 Iconography

- Consistent icon set (Material Design icons)
- Icon sizes:
  - Navigation icons: 24dp
  - List item icons: 24dp
  - Small UI icons: 16dp
  - Large feature icons: 32dp
- Icon colors follow color palette
- Use outlined style for general UI
- Use filled style for active/selected states
- **Sensor Type Icons**:
  - Motion sensor: Person walking icon
  - Temperature sensor: Thermometer icon
  - Humidity sensor: Water droplet icon
  - Light sensor: Sun/brightness icon
  - Air quality sensor: Air flow icon
  - Sound sensor: Sound wave icon
  - Contact sensor: Door/window icon

### 5.5 Layout Guidelines

- Grid system: 8dp baseline grid
- Standard margins: 16dp
- Content padding: 16dp
- List item height: 72dp (with icon and secondary text)
- Vertical spacing between sections: 24dp
- Use responsive layout techniques:
  - Single column layout on phones
  - Two-column layout on tablets
  - Adaptive cards and grids

## 6. Status & Feedback Systems

### 6.1 Connection Status Indicators

- **Online Status**:
  - Green dot indicator
  - "Connected" text
  - Connection type icon (WiFi/Bluetooth)
  - Signal strength indicator (if applicable)
- **Offline Status**:
  - Red dot indicator
  - "Disconnected" text
  - Last seen timestamp
  - "Reconnect" button
- **Connecting Status**:
  - Yellow dot indicator with pulsing animation
  - "Connecting..." text
  - Progress indicator
- **Error Status**:
  - Red dot with exclamation mark
  - Error message
  - Troubleshooting button

### 6.2 User Action Feedback

- **Loading States**:
  - Circular progress for indeterminate operations
  - Linear progress for determinate operations
  - Skeleton screens for content loading
  - Transparent overlay for modal loading
- **Success Feedback**:
  - Green checkmark animation
  - Success toast notification (2s display)
  - Haptic feedback (subtle vibration)
  - Success sound (optional, respects system settings)
- **Error Feedback**:
  - Red error icon
  - Error toast or dialog with explanation
  - Haptic feedback (error pattern)
  - Retry option when applicable
- **Empty States**:
  - Illustrative graphics
  - Helpful text explaining the empty state
  - Suggestion for next action
  - Primary CTA button

### 6.3 System Notifications

- **Push Notifications**:
  - LightBox connection changes
  - Scheduled events starting
  - Firmware updates available
  - System alerts requiring attention
- **In-App Notifications**:
  - Toast messages for transient information
  - Banner notifications for important alerts
  - Notification center for history
  - Badge counters on navigation items

## 7. Accessibility Considerations

### 7.1 Visual Accessibility

- **Contrast Ratios**:
  - Text meets WCAG AA standard (4.5:1 for normal text, 3:1 for large text)
  - UI components have sufficient contrast from background
- **Text Scaling**:
  - UI supports text size increase up to 200%
  - Layouts adapt to text size changes
- **Color Independence**:
  - Information not conveyed by color alone
  - Alternative indicators (icons, patterns) supplement color
- **Dark Mode Support**:
  - Complete dark theme for all screens
  - Reduced brightness for nighttime usage

### 7.2 Interactive Accessibility

- **Touch Targets**:
  - Minimum size of 48dp x 48dp
  - Adequate spacing between targets (8dp minimum)
- **Gesture Alternatives**:
  - Button alternatives for gestures
  - Simple interaction patterns
- **Focus Indicators**:
  - Visible focus state for all interactive elements
  - Logical focus order for keyboard navigation
- **Screen Reader Support**:
  - All UI elements have appropriate content descriptions
  - Custom components implement accessibility interfaces
  - Live regions for dynamic content

### 7.3 Cognitive Accessibility

- **Clear Labeling**:
  - Descriptive button labels
  - Explanatory helper text
  - Iconography paired with text
- **Progressive Disclosure**:
  - Complex features revealed gradually
  - Advanced options in expandable sections
- **Error Prevention**:
  - Confirmation for destructive actions
  - Clear error messages with solutions
  - Undo functionality where appropriate

## 8. Performance Expectations

### 8.1 Loading Time Standards

- App cold start: Under 2 seconds
- Screen transitions: Under 300ms
- LED state updates: Under 100ms local, under 500ms remote
- Pattern application: Under 200ms
- Animation playback: 60fps minimum

### 8.2 Responsiveness Standards

- Touch response: Under 100ms
- Slider/control updates: Real-time (no perceivable lag)
- Color selection updates: Real-time preview
- Keyboard input: No typing lag

### 8.3 Offline Performance

- Seamless transition between online/offline modes
- Offline capabilities clearly indicated
- Appropriate caching of patterns and settings
- Background synchronization when connection restored

### 8.4 Battery Optimization

- Efficient Bluetooth connection management
- Background activity minimization
- Appropriate refresh rates for UI updates
- Power-saving mode support

### 8.5 Sensor Responsiveness

- Sensor data refresh: Under 5 seconds for dashboard
- Data graph loading: Under 2 seconds for 24h of data
- Sensor command execution: Under 1 second
- Rule trigger to action: Under 500ms for local rules
- Historical data query: Under 3 seconds for 30 days of data
- Multiple sensor aggregation: Under 2 seconds for dashboard view
