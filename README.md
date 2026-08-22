# Frog Rock Classic - Firebase Setup Guide

## Setting up Real-time Score Updates

To enable live score synchronization across multiple devices, you need to set up Firebase Realtime Database.

### Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" (or select existing project)
3. Enter project name: `frog-rock-classic`
4. Enable Google Analytics (optional)
5. Click "Create project"

### Step 2: Set up Realtime Database

1. In your Firebase project, go to "Realtime Database"
2. Click "Create Database"
3. Choose "Start in test mode" (for development)
4. Select a location close to your users
5. Click "Done"

### Step 3: Get Firebase Configuration

1. Click the gear icon → "Project settings"
2. Scroll down to "Your apps" section
3. Click "Add app" → Web icon (</>)
4. Register app with name: "Frog Rock Classic"
5. Copy the Firebase config object

### Step 4: Update scores.html

Replace the placeholder Firebase config in `scores.html` with your actual config:

```javascript
const firebaseConfig = {
    apiKey: "your-actual-api-key",
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.firebaseio.com",
    projectId: "your-project-id",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "your-app-id"
};
```

### Step 5: Deploy and Test

1. Push your changes to GitHub
2. Open the scores page on multiple devices/browsers
3. Submit scores on one device - they should appear instantly on all others!

## Security Note

For production use, update your Firebase Database rules to restrict access:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Consider adding authentication for tournament organizers only.

## Troubleshooting

- **Connection issues**: Check Firebase config is correct
- **No updates**: Verify database URL and permissions
- **Slow updates**: Check internet connection

The live updates use Firebase's real-time listeners, so changes sync instantly across all connected devices!</content>
<parameter name="filePath">c:\Users\chcom\OneDrive\Documents\VsCodeFilesFolders\Frog Rock Classic\FIREBASE_SETUP.md