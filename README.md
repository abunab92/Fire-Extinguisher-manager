# Fire Extinguisher Manager

A comprehensive mobile application for managing fire extinguishers in factory environments, built with Flutter.

**Proudly made by: Mohammad Abunab**

## Features

### 🔥 Core Fire Extinguisher Management
- **Add, Edit, Delete** fire extinguisher records
- **Location tracking** with free-text location fields
- **Type classification** (CO2, Foam, Powder, etc.)
- **Expiry date monitoring** with visual indicators
- **Status management** (Active, Needs Refill, Out of Service)
- **Color-coded status indicators** for quick visual assessment

### 🔐 Microsoft Account Integration
- **Secure authentication** using Azure Active Directory OAuth2
- **Automatic token refresh** for seamless user experience
- **User session management** with persistent login
- **Professional login interface** with Microsoft branding

### ☁️ OneDrive Cloud Synchronization
- **Automatic data backup** to OneDrive
- **Real-time synchronization** across multiple devices
- **Conflict resolution** for concurrent edits
- **Structured cloud storage** in dedicated app folders
- **Offline support** with automatic sync when online

### 📊 Excel Import/Export
- **Export to Excel** with professional formatting
- **Import from Excel** with intelligent column detection
- **UTF-8 compatibility** for international characters
- **Multiple date format support** (DD/MM/YYYY, MM/DD/YYYY, YYYY-MM-DD)
- **Template generation** for easy data entry
- **Color-coded expiry status** in exported files
- **Summary statistics** included in exports

### 🔔 Smart Notification System
- **Automatic scheduling** for all fire extinguishers
- **Multi-level alerts**: 30 days, 7 days, and expiry day
- **Critical notifications** for overdue extinguishers
- **Background notifications** that work when app is closed
- **Customizable notification settings**
- **Professional notification management interface**

### 📱 Professional User Interface
- **Material Design 3** with fire safety color scheme
- **Responsive design** for phones and tablets
- **Touch-friendly interface** optimized for mobile use
- **Intuitive navigation** with clear visual hierarchy
- **Professional branding** suitable for industrial environments

## Technical Specifications

### Platform Support
- **Android**: Minimum SDK 21 (Android 5.0+)
- **Target SDK**: Latest Android version
- **Architecture**: ARM64, ARMv7, x86_64

### Dependencies
- **Flutter**: 3.35.1 (stable channel)
- **Dart**: Latest stable version
- **Key Packages**:
  - `provider`: State management
  - `aad_oauth`: Microsoft authentication
  - `microsoft_graph_api`: OneDrive integration
  - `excel`: Excel file processing
  - `awesome_notifications`: Notification system
  - `file_picker`: File selection
  - `share_plus`: File sharing
  - `path_provider`: Local storage

### Security Features
- **Secure token storage** using Android Keystore
- **OAuth2 authentication** with Microsoft Azure AD
- **Encrypted local data storage**
- **Secure network communications** (HTTPS only)
- **Permission-based access control**

## Installation & Setup

### Prerequisites
1. **Flutter SDK** (3.35.1 or later)
2. **Android Studio** or **VS Code** with Flutter extensions
3. **Android SDK** (API level 21+)
4. **Java Development Kit** (JDK 11 or later)

### Building the APK

1. **Clone the project**:
   ```bash
   git clone <repository-url>
   cd fire_extinguisher_app
   ```

2. **Install dependencies**:
   ```bash
   flutter pub get
   ```

3. **Configure Android signing** (for release builds):
   - Create a keystore file
   - Update `android/app/build.gradle` with signing configuration

4. **Build the APK**:
   ```bash
   # Debug APK (for testing)
   flutter build apk --debug
   
   # Release APK (for production)
   flutter build apk --release
   ```

5. **Locate the APK**:
   - Debug: `build/app/outputs/flutter-apk/app-debug.apk`
   - Release: `build/app/outputs/flutter-apk/app-release.apk`

### Microsoft Azure Configuration

To enable Microsoft Account authentication:

1. **Register your app** in Azure Active Directory
2. **Configure redirect URIs** for mobile application
3. **Update authentication settings** in `lib/services/auth_service.dart`
4. **Add your client ID** and tenant information

## Usage Guide

### First Time Setup
1. **Install the APK** on your Android device
2. **Grant permissions** for notifications and file access
3. **Sign in** with your Microsoft Account
4. **Enable notifications** for expiry alerts

### Managing Fire Extinguishers
1. **Add new extinguishers** using the + button
2. **Edit existing records** by tapping the menu on each item
3. **Update status** as needed (Active, Needs Refill, Out of Service)
4. **Monitor expiry dates** with color-coded indicators

### Data Management
1. **Export data** to Excel for reporting and backup
2. **Import data** from existing Excel files
3. **Sync with OneDrive** for multi-device access
4. **Share reports** via email or other apps

### Notifications
1. **Configure notification settings** in the app menu
2. **Receive automatic alerts** for upcoming expiries
3. **Test notifications** to ensure proper functionality
4. **Manage notification schedule** (30 days, 7 days, expiry day)

## File Structure

```
lib/
├── main.dart                           # App entry point
├── models/
│   └── fire_extinguisher.dart         # Data model
├── services/
│   ├── extinguisher_service.dart      # Local data management
│   ├── auth_service.dart               # Microsoft authentication
│   ├── onedrive_service.dart           # Cloud synchronization
│   ├── excel_service.dart              # Excel import/export
│   └── notification_service.dart      # Notification management
└── screens/
    ├── login_screen.dart               # Authentication UI
    ├── home_screen.dart                # Main app interface
    ├── add_edit_extinguisher_screen.dart # Add/edit form
    ├── import_export_screen.dart       # Data management
    ├── notifications_screen.dart       # Notification settings
    └── about_screen.dart               # App information
```

## Permissions

The app requires the following Android permissions:

- **INTERNET**: For cloud synchronization and authentication
- **ACCESS_NETWORK_STATE**: To check network connectivity
- **RECEIVE_BOOT_COMPLETED**: For persistent notifications
- **WAKE_LOCK**: For critical notifications
- **VIBRATE**: For notification alerts
- **USE_FULL_SCREEN_INTENT**: For urgent notifications
- **SCHEDULE_EXACT_ALARM**: For precise notification timing
- **READ/WRITE_EXTERNAL_STORAGE**: For Excel file operations

## Troubleshooting

### Common Issues

1. **Build Errors**:
   - Ensure Flutter SDK is properly installed
   - Run `flutter doctor` to check for issues
   - Clean build cache: `flutter clean`

2. **Authentication Issues**:
   - Verify Azure AD configuration
   - Check internet connectivity
   - Ensure correct client ID and tenant settings

3. **Notification Problems**:
   - Grant notification permissions in device settings
   - Check battery optimization settings
   - Verify notification channel configuration

4. **Sync Issues**:
   - Ensure Microsoft Account has OneDrive access
   - Check network connectivity
   - Verify authentication token validity

### Support

For technical support or feature requests, please contact the development team.

## License

This application is proprietary software developed for factory fire safety management.

## Credits

**Developed by**: Mohammad Abunab  
**Framework**: Flutter  
**Platform**: Android  
**Cloud Services**: Microsoft OneDrive  
**Authentication**: Azure Active Directory  

---

*Fire Extinguisher Manager - Ensuring factory safety through smart technology*

