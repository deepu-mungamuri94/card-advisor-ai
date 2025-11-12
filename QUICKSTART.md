# 🚀 Quick Start Guide - Card Advisor AI

This guide will help you set up and start using Card Advisor AI in under 10 minutes.

---

## 📋 Prerequisites Checklist

Before you begin, ensure you have:

- [ ] **Android Studio** (Narwhal 2025.1.2 or later) - [Download here](https://developer.android.com/studio)
- [ ] **Node.js** (v16 or later) - [Download here](https://nodejs.org/)
- [ ] **Android device** or emulator (Android 7.0+)
- [ ] **Google Gemini API Key** - [Get free key](https://aistudio.google.com/app/apikey)
- [ ] **USB cable** (for device installation)

---

## ⚡ Installation Steps

### Step 1: Get Google Gemini API Key (2 minutes)

1. **Visit**: [Google AI Studio](https://aistudio.google.com/app/apikey)

2. **Sign in** with your Google account

3. **Click "Create API Key"**

4. **Copy the key** (starts with `AIza...`)

5. **Save it** somewhere safe (you'll need it later)

💡 **Note**: Free tier includes 1,500 requests/day - more than enough!

---

### Step 2: Set Up Project (3 minutes)

#### Option A: Using Terminal (Recommended)

```bash
# Navigate to project directory
cd /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp

# Install Capacitor CLI globally (if not already installed)
npm install -g @capacitor/cli

# Copy web assets to Android
npx cap copy android
```

**Expected output:**
```
✔ Copying web assets from www to android/app/src/main/assets/public in 3ms
✔ Creating capacitor.config.json in android/app/src/main/assets in 0.5ms
✔ copy android in 6ms
```

#### Option B: Manual Check

Verify files are in place:
```
android/app/src/main/assets/public/index.html  ← Should exist
android/app/src/main/assets/capacitor.config.json  ← Should exist
```

---

### Step 3: Open in Android Studio (1 minute)

#### Option A: Command Line

```bash
# From project root
open -a "Android Studio" ./android
```

#### Option B: Using Android Studio UI

1. **Launch Android Studio**
2. **File** → **Open**
3. **Navigate to**: `/Users/dmungamuri/AndroidStudioProjects/cardadvisorapp/android`
4. **Click "Open"**

⚠️ **Critical**: Open the `android` folder, NOT the root `cardadvisorapp` folder!

---

### Step 4: Build the App (2 minutes)

#### In Android Studio:

1. **Wait for Gradle sync** to complete (status bar bottom)

2. **Build APK**:
   - **Build** → **Build Bundle(s) / APK(s)** → **Build APK(s)**

3. **Wait for build** (1-2 minutes on first build)

4. **Success notification** will appear:
   ```
   APK(s) generated successfully for 1 module:
   Module 'app': locate or analyze the APK
   ```

5. **Click "locate"** to find the APK

6. **APK location**:
   ```
   android/app/build/outputs/apk/debug/app-debug.apk
   ```

#### OR via Command Line:

```bash
cd android
./gradlew assembleDebug
```

APK will be at: `android/app/build/outputs/apk/debug/app-debug.apk`

---

## 📲 Install on Device

### Method 1: Direct Install via USB (Fastest)

#### Enable Developer Mode on Phone:

1. **Settings** → **About phone**
2. **Tap "Build number"** 7 times
3. **Developer options** will appear in Settings

#### Enable USB Debugging:

1. **Settings** → **Developer options**
2. **Toggle "USB debugging"** ON
3. **Confirm** the popup

#### Install App:

1. **Connect phone** to computer via USB
2. **Authorize computer** (popup on phone)
3. **In Android Studio**: Click green **▶️ Run** button
4. **Select your device** from dropdown
5. **App installs and launches**

---

### Method 2: Install APK via Google Drive (No USB)

#### Upload to Drive:

1. **Locate APK**:
   ```
   android/app/build/outputs/apk/debug/app-debug.apk
   ```

2. **Upload to Google Drive**

3. **Share link** with yourself or just keep it in your Drive

#### Download on Phone:

1. **Open Google Drive** on your phone
2. **Find app-debug.apk**
3. **Tap to download**
4. **You may see warning** - "This type of file can harm your device"
5. **Tap "Download anyway"**

#### Install APK:

1. **Open notification** or **Files app**
2. **Tap app-debug.apk**
3. **Chrome/Files warning**: "Install unknown apps"
4. **Tap "Settings"**
5. **Toggle "Allow from this source"** ON
6. **Tap back**, then **Install**
7. **Open** when installation completes

---

### Method 3: ADB Command (For Developers)

```bash
# Ensure device is connected and authorized
adb devices

# Install APK
adb install android/app/build/outputs/apk/debug/app-debug.apk

# If already installed, use -r to replace
adb install -r android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 🎯 First-Time App Setup (2 minutes)

### 1. Launch the App

- **Tap** Card Advisor AI icon on your phone
- **Grant permissions** if asked (only INTERNET)

### 2. Configure API Key

1. **Tap hamburger menu** (☰) in top-left

2. **Tap "Settings"**

3. **Paste your Gemini API key**
   - The key you got from Step 1
   - Input is masked (type="password") for security

4. **Tap "Save API Key"**

5. **Success notification** appears

### 3. Add Your First Card

1. **Open menu** (☰) → **My Cards**

2. **Enter exact card name** in text field:
   ```
   Examples (use exact names):
   - HDFC Millennia Credit Card
   - SBI Cashback Credit Card
   - ICICI Amazon Pay Credit Card
   - Axis Magnus Credit Card
   - AMEX Platinum Travel Credit Card
   ```

3. **Tap "Fetch & Save Card Rules"**

4. **Wait 4-8 seconds** (loading indicator shows)

5. **AI fetches comprehensive rules** from bank website:
   - Base reward rates
   - 70+ spending categories
   - Movie tickets (BookMyShow offers)
   - Dining & food delivery
   - Travel benefits (lounge, insurance)
   - Grocery rewards
   - Fuel surcharge waivers
   - OTT subscriptions
   - Utilities & bills
   - And much more!

6. **Card appears** in your portfolio below

7. **Repeat** for all your cards

### 4. View Card Details

1. **Tap the purple eye icon** (👁️) on any card

2. **Scrollable modal** opens with complete rules

3. **Scroll through** all the benefits

4. **Optional**: Tap "Reload Rules" to refresh from bank website

5. **Close** by tapping "Close" button or outside modal

### 5. Get Your First Recommendation

1. **Open menu** (☰) → **AI Advisor**

2. **Describe your purchase**:
   ```
   Examples:
   - "Buying ₹5,000 groceries at BigBasket"
   - "Booking flight tickets for ₹15,000"
   - "Shopping on Amazon for ₹3,000"
   - "Paying electricity bill of ₹2,500"
   - "Dining at restaurant for ₹1,200"
   ```

3. **Tap "Get Best Card Suggestion"**

4. **AI analyzes** all your cards (takes 3-6 seconds)

5. **Get detailed recommendation**:
   - 💳 Best card to use
   - 💰 Expected reward amount
   - 📊 Calculation breakdown
   - 🔄 Alternative cards (if close)

6. **Usage stats** appear as toast (auto-dismisses):
   ```
   ✓ 1 request • 2,450 tokens
     Prompt: 1,200 • Response: 1,250
   ```

---

## 🎓 Usage Tips

### Adding Cards

**✅ Do**:
- Use exact bank/card name
- Include "Credit Card" in name
- Example: "HDFC Millennia Credit Card"

**❌ Don't**:
- Use abbreviations ("HDFC Mill")
- Add numbers ("Card 1")
- Use nicknames ("My HDFC")

### Getting Recommendations

**✅ Do**:
- Be specific about amount
- Mention merchant/category
- Example: "₹5,000 at BigBasket"

**❌ Don't**:
- Be vague ("some shopping")
- Skip amount
- Example: "buying stuff"

### Keeping Rules Updated

**When to Refresh**:
- Bank announces new offers
- Quarterly benefit changes
- Devaluation notices
- You notice outdated info

**How to Refresh**:
- **From list**: Tap 🔄 icon on card
- **From modal**: Tap "Reload Rules" button

---

## 🐛 Troubleshooting Setup Issues

### Issue: "Default activity not found"

**Problem**: Opened wrong Android folder

**Solution**:
1. Close Android Studio
2. **File** → **Open**
3. Navigate to: `/Users/dmungamuri/AndroidStudioProjects/cardadvisorapp/android`
4. Select **android** folder, not root folder
5. Click "Open"

---

### Issue: App shows blank white screen

**Problem**: Web assets not copied to Android

**Solution**:
```bash
cd /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp
npx cap copy android
# Rebuild in Android Studio
```

---

### Issue: API key not working

**Symptoms**: "Failed to fetch rules", "API error"

**Solutions**:

1. **Verify key format**:
   - Should start with `AIza`
   - Length: ~39 characters
   - No spaces or line breaks

2. **Check API status**:
   - Visit [Google AI Studio](https://aistudio.google.com)
   - Try your key in the playground
   - Ensure Gemini API is enabled

3. **Clear and re-enter**:
   - Menu → Settings
   - Delete current key
   - Paste again carefully
   - Save

4. **Generate new key**:
   - If old key doesn't work
   - Create new one at Google AI Studio
   - Use the new key

---

### Issue: "Rate limit exceeded" (429 error)

**Problem**: Too many requests too fast

**Solution**:
- **Wait 60 seconds**
- App automatically retries
- Check quota at [Google AI Studio](https://aistudio.google.com)
- Free tier: 15 requests/minute, 1,500/day

---

### Issue: Can't install APK on phone

**Problem**: "Install blocked" or "Unknown sources"

**Solution**:
1. **Settings** → **Security**
2. **Toggle "Unknown sources"** ON
   - OR:
3. **Settings** → **Apps** → **Chrome/Files**
4. **Toggle "Install unknown apps"** ON

---

### Issue: Build fails in Android Studio

**Problem**: Gradle sync errors, build errors

**Solutions**:

1. **Clean project**:
   ```bash
   cd android
   ./gradlew clean
   ```

2. **Invalidate caches**:
   - **File** → **Invalidate Caches**
   - Check all boxes
   - **Invalidate and Restart**

3. **Re-sync Gradle**:
   - **File** → **Sync Project with Gradle Files**

4. **Update Gradle** (if prompted):
   - Click "Update" in notification

---

### Issue: Header/menu hidden behind status bar

**Already fixed!** Safe area insets applied.

**If still seeing issue**:
```bash
# Ensure you have latest code
cd /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp
git pull origin main
npx cap copy android
# Rebuild
```

---

### Issue: Rules don't show movie tickets/dining offers

**Already fixed!** AI now explicitly fetches 70+ categories.

**If still missing**:
1. **Refresh card rules** (tap 🔄 icon)
2. **Wait for AI** to re-fetch from bank website
3. **Check modal view** (tap 👁️) - scroll through all sections

---

## 🎉 Next Steps

### You're All Set!

Now you can:

1. ✅ **Add more cards** to your portfolio
2. ✅ **Get recommendations** for every purchase
3. ✅ **Maximize rewards** on all spending
4. ✅ **Track API usage** via toast notifications
5. ✅ **Keep rules updated** with refresh buttons

### Explore More

- **View full documentation**: [README.md](README.md)
- **Understand architecture**: [ARCHITECTURE.md](ARCHITECTURE.md)
- **Check GitHub**: [Repository](https://github.com/deepu-mungamuri94/card-advisor-ai)

---

## 📞 Need Help?

1. **Re-read this guide** - Most issues covered here
2. **Check main README** - Detailed feature explanations
3. **Use Chrome DevTools** - `chrome://inspect` for debugging
4. **Check console logs** - See what's happening
5. **Open GitHub issue** - Report bugs or request features

---

**Happy spending & maximizing rewards!** 💳✨

