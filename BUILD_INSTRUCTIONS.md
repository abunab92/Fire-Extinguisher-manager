# Build Instructions for Fire Extinguisher Manager

This document provides step-by-step instructions for building the Fire Extinguisher Manager APK on your local development machine.

## Prerequisites

### 1. Install Flutter SDK

1. **Download Flutter**:
   - Visit [flutter.dev](https://flutter.dev/docs/get-started/install)
   - Download the Flutter SDK for your operating system
   - Extract to a suitable location (e.g., `C:\flutter` on Windows, `/usr/local/flutter` on macOS/Linux)

2. **Add Flutter to PATH**:
   ```bash
   # Windows (add to System Environment Variables)
   C:\flutter\bin
   
   # macOS/Linux (add to ~/.bashrc or ~/.zshrc)
   export PATH="$PATH:/usr/local/flutter/bin"
   ```

3. **Verify Installation**:
   ```bash
   flutter --version
   flutter doctor
   ```

### 2. Install Android Studio

1. **Download Android Studio**:
   - Visit [developer.android.com/studio](https://developer.android.com/studio)
   - Download and install Android Studio

2. **Install Android SDK**:
   - Open Android Studio
   - Go to Tools → SDK Manager
   - Install Android SDK (API level 21 or higher)
   - Install Android SDK Build-Tools
   - Install Android SDK Platform-Tools

3. **Configure Environment Variables**:
   ```bash
   # Windows
   ANDROID_HOME=C:\Users\%USERNAME%\AppData\Local\Android\Sdk
   
   # macOS
   export ANDROID_HOME=$HOME/Library/Android/sdk
   
   # Linux
   export ANDROID_HOME=$HOME/Android/Sdk
   ```

### 3. Install Java Development Kit (JDK)

1. **Install JDK 11 or later**:
   - Download from [Oracle](https://www.oracle.com/java/technologies/downloads/) or use OpenJDK
   - Install and configure JAVA_HOME environment variable

2. **Verify Installation**:
   ```bash
   java -version
   javac -version
   ```

## Building the APK

### 1. Prepare the Project

1. **Extract the project files** to your desired location
2. **Open terminal/command prompt** in the project directory
3. **Install dependencies**:
   ```bash
   flutter pub get
   ```

### 2. Configure Microsoft Azure (Optional)

If you want to enable Microsoft Account authentication:

1. **Register your app** in Azure Active Directory:
   - Go to [Azure Portal](https://portal.azure.com)
   - Navigate to Azure Active Directory → App registrations
   - Click "New registration"
   - Set redirect URI for mobile application

2. **Update configuration**:
   - Open `lib/services/auth_service.dart`
   - Replace placeholder values with your Azure AD configuration:
     ```dart
     static const String clientId = 'YOUR_CLIENT_ID';
     static const String tenantId = 'YOUR_TENANT_ID';
     ```

### 3. Build Debug APK (for testing)

```bash
flutter build apk --debug
```

The debug APK will be located at:
`build/app/outputs/flutter-apk/app-debug.apk`

### 4. Build Release APK (for production)

#### Option A: Using Debug Signing (Quick)
```bash
flutter build apk --release
```

#### Option B: Using Custom Signing (Recommended for production)

1. **Create a keystore**:
   ```bash
   keytool -genkey -v -keystore ~/upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
   ```

2. **Create key.properties file**:
   Create `android/key.properties`:
   ```properties
   storePassword=<password from previous step>
   keyPassword=<password from previous step>
   keyAlias=upload
   storeFile=<location of the key store file, such as /Users/<user name>/upload-keystore.jks>
   ```

3. **Update build.gradle**:
   Edit `android/app/build.gradle.kts` to include signing configuration:
   ```kotlin
   android {
       // ... existing configuration
       
       signingConfigs {
           release {
               keyAlias keystoreProperties['keyAlias']
               keyPassword keystoreProperties['keyPassword']
               storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
               storePassword keystoreProperties['storePassword']
           }
       }
       
       buildTypes {
           release {
               signingConfig signingConfigs.release
           }
       }
   }
   ```

4. **Build signed APK**:
   ```bash
   flutter build apk --release
   ```

The release APK will be located at:
`build/app/outputs/flutter-apk/app-release.apk`

## Troubleshooting

### Common Build Issues

1. **Flutter Doctor Issues**:
   ```bash
   flutter doctor
   ```
   Follow the suggestions to resolve any issues.

2. **Gradle Build Failures**:
   ```bash
   cd android
   ./gradlew clean
   cd ..
   flutter clean
   flutter pub get
   ```

3. **Android License Issues**:
   ```bash
   flutter doctor --android-licenses
   ```
   Accept all licenses when prompted.

4. **Memory Issues**:
   Add to `android/gradle.properties`:
   ```properties
   org.gradle.jvmargs=-Xmx4g -XX:MaxMetaspaceSize=512m -XX:+HeapDumpOnOutOfMemoryError
   ```

### Platform-Specific Issues

#### Windows
- Ensure Windows Defender doesn't block Flutter/Android tools
- Use PowerShell or Command Prompt as Administrator if needed
- Check that all paths don't contain spaces or special characters

#### macOS
- Install Xcode command line tools: `xcode-select --install`
- Ensure proper permissions for Android SDK directory
- Use Homebrew for easier package management

#### Linux
- Install required libraries:
  ```bash
  sudo apt-get install curl git unzip xz-utils zip libglu1-mesa
  ```
- Ensure proper permissions for Android SDK directory

## Testing the APK

### 1. Install on Android Device

1. **Enable Developer Options**:
   - Go to Settings → About Phone
   - Tap "Build Number" 7 times
   - Go back to Settings → Developer Options
   - Enable "USB Debugging"

2. **Install APK**:
   ```bash
   # Via ADB
   adb install build/app/outputs/flutter-apk/app-release.apk
   
   # Or transfer APK to device and install manually
   ```

### 2. Test Core Features

1. **Launch the app** and verify it opens correctly
2. **Test fire extinguisher management**:
   - Add new extinguisher
   - Edit existing record
   - Delete record
3. **Test notifications** (if enabled)
4. **Test Excel export/import** (if files are available)
5. **Test Microsoft Account login** (if configured)

## Performance Optimization

### 1. App Size Optimization

Build separate APKs for different architectures:
```bash
flutter build apk --split-per-abi
```

This creates separate APKs for:
- `app-arm64-v8a-release.apk` (64-bit ARM)
- `app-armeabi-v7a-release.apk` (32-bit ARM)
- `app-x86_64-release.apk` (64-bit x86)

### 2. Build Optimization

For faster builds during development:
```bash
flutter build apk --debug --fast-start
```

## Distribution

### Google Play Store
1. Create a Google Play Console account
2. Upload the signed APK
3. Complete store listing information
4. Submit for review

### Direct Distribution
1. Host the APK on your server
2. Provide download link to users
3. Users must enable "Install from Unknown Sources"

## Support

For build issues or questions:
1. Check Flutter documentation: [flutter.dev/docs](https://flutter.dev/docs)
2. Review Android documentation: [developer.android.com](https://developer.android.com)
3. Search Flutter GitHub issues: [github.com/flutter/flutter/issues](https://github.com/flutter/flutter/issues)

---

**Note**: This project is configured for Android only. iOS support would require additional setup with Xcode and Apple Developer account.

