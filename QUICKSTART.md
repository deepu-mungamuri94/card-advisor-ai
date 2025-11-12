# 🚀 Quick Start Guide - Card Advisor AI

## 5-Minute Setup

### Step 1: Build the APK (2 minutes)

1. **Open Android Studio**
2. **File** → **Open** → Select: `/Users/dmungamuri/AndroidStudioProjects/cardadvisorapp/android`
3. **Build** → **Build APK(s)**
4. Click **"locate"** when done
5. Upload `app-debug.apk` to Google Drive

### Step 2: Install on Phone (1 minute)

1. Download APK from Drive on your phone
2. Tap to install
3. Allow installation from Chrome/Files if prompted

### Step 3: Configure API Key (2 minutes)

1. **Get API Key**:
   - Visit: https://aistudio.google.com/app/apikey
   - Sign in with Google
   - Click "Create API Key"
   - Copy the key (starts with `AIza`)

2. **Add to App**:
   - Open Card Advisor AI
   - Click ⚙️ (Settings) icon
   - Paste API key
   - Click "Save"

### Step 4: Add Your First Card (30 seconds)

1. Go to **"My Cards"** tab
2. Type card name: "HDFC Millennia"
3. Click **"Fetch & Save Card Rules"**
4. Done! Card rules saved.

### Step 5: Get Your First Recommendation (30 seconds)

1. Go to **"Advisor"** tab
2. Type: "Buying groceries for ₹5,000"
3. Click **"Get Best Card Suggestion"**
4. See which card gives max rewards! 💰

---

## That's It! 🎉

You're now ready to maximize your credit card rewards!

---

## Quick Commands

```bash
# Copy web changes to Android
npx cap copy android

# Build APK via command line
cd android && ./gradlew assembleDebug

# Install via ADB
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

---

## Need Help?

See the full [README.md](README.md) for detailed documentation.

