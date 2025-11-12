# 💳 Card Advisor AI

> An intelligent Android app that helps you maximize credit card rewards by analyzing your card portfolio and suggesting the best card for each purchase.

[![Android](https://img.shields.io/badge/Android-Capacitor-green.svg)](https://capacitorjs.com/)
[![Gemini API](https://img.shields.io/badge/AI-Google%20Gemini-blue.svg)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📱 Overview

**Card Advisor AI** is a mobile application that leverages Google's Gemini AI to provide intelligent credit card recommendations. It fetches real-time card reward rules from official bank websites and suggests the optimal card for your purchases, helping you maximize cashback and reward points.

### Key Features

- 🤖 **AI-Powered Recommendations** - Uses Gemini 2.5 Flash with Google Search
- 💾 **Offline Storage** - Cards stored locally using localStorage
- 🔄 **Real-Time Updates** - Fetches latest rules from official bank websites
- 🇮🇳 **India-Focused** - Optimized for Indian credit cards and currency
- 📊 **Usage Analytics** - Track API requests and token consumption
- 🎨 **Modern UI** - Beautiful Tailwind CSS design with tabbed interface
- 🔒 **Secure** - API keys stored locally, never shared

---

## 🏗️ Architecture

### Technology Stack

| Component | Technology |
|-----------|------------|
| **Frontend** | HTML5, JavaScript (ES6+), Tailwind CSS |
| **Mobile Runtime** | Capacitor (Web-to-Native) |
| **Platform** | Android (Native) |
| **AI Engine** | Google Gemini 2.5 Flash API |
| **Storage** | localStorage (Browser API) |
| **Build System** | Gradle, Android Studio |

### Project Structure

```
cardadvisorapp/
├── android/                    # Native Android project
│   ├── app/
│   │   ├── src/main/
│   │   │   ├── assets/public/  # Web assets (auto-generated)
│   │   │   ├── java/           # MainActivity.java
│   │   │   └── res/            # Android resources
│   │   └── build.gradle
│   └── gradle/
├── www/                        # Web application source
│   └── index.html              # Main app (1169 lines)
├── capacitor.config.json       # Capacitor configuration
└── README.md                   # This file
```

---

## 🚀 Getting Started

### Prerequisites

- **Android Studio** (Narwhal 2025.1.2 or later)
- **Node.js** (v16+ recommended)
- **Capacitor CLI** (`npm install -g @capacitor/cli`)
- **Google Gemini API Key** ([Get it here](https://aistudio.google.com/app/apikey))

### Installation Steps

#### 1. Clone the Repository

```bash
cd /path/to/your/projects
# Project already exists at:
cd /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp
```

#### 2. Install Dependencies

```bash
# Install Capacitor CLI globally (if not already installed)
npm install -g @capacitor/cli

# No package.json needed - it's a pure HTML/JS app
```

#### 3. Copy Web Assets to Android

```bash
# Copy www/ folder contents to Android assets
npx cap copy android
```

This command copies:
- `www/index.html` → `android/app/src/main/assets/public/index.html`
- `capacitor.config.json` → Android assets

#### 4. Open in Android Studio

```bash
# Option A: Command line
open -a "Android Studio" ./android

# Option B: In Android Studio
# File → Open → Navigate to:
# /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp/android
```

⚠️ **Important**: Open the `android` folder, NOT the root `cardadvisorapp` folder!

#### 5. Build the APK

**In Android Studio:**

1. **Build** → **Build Bundle(s) / APK(s)** → **Build APK(s)**
2. Wait for build to complete (1-2 minutes)
3. Click **"locate"** in the notification
4. APK location: `android/app/build/outputs/apk/debug/app-debug.apk`

**OR via Command Line:**

```bash
cd android
./gradlew assembleDebug
```

APK will be at: `android/app/build/outputs/apk/debug/app-debug.apk`

---

## 📲 Installing on Device

### Method 1: Direct Install via USB

1. **Enable Developer Options** on your phone:
   - Settings → About phone → Tap "Build number" 7 times

2. **Enable USB Debugging**:
   - Settings → Developer options → Enable "USB debugging"

3. **Connect phone** via USB cable

4. **In Android Studio**: Click the green ▶️ Run button

5. **Select your device** from the dropdown

### Method 2: Install APK via Google Drive

1. **Upload** `app-debug.apk` to Google Drive

2. **Download** on your phone

3. **Install**:
   - Tap the APK file
   - Allow installation from Chrome/Files
   - Tap "Install"

### Method 3: ADB Command

```bash
# Connect device via USB
adb devices

# Install APK
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 🎯 How to Use

### First-Time Setup

1. **Launch App** - Open "Card Advisor AI"

2. **Configure API Key**:
   - Click ⚙️ (Settings) icon in top-right
   - Get API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
   - Paste key and click "Save API Key"
   - Key is stored locally and never shared

### Adding Your Credit Cards

1. **Go to "My Cards" tab** (top navigation)

2. **Enter card name**:
   - Example: "HDFC Millennia"
   - Example: "SBI Pulse"
   - Example: "ICICI Amazon Pay"

3. **Click "Fetch & Save Card Rules"**

4. **AI fetches rules** from official bank website:
   - Reward rates (e.g., 5% on Amazon)
   - Exclusions (e.g., no rewards on rent)
   - Redemption values

5. **View saved cards** in portfolio below

### Managing Cards

- **View Rules**: Click "View Rules" on any card
- **Update Rules**: Click 🔄 (Refresh) icon - fetches latest data
- **Rename Card**: Click ✏️ (Edit) icon
- **Delete Card**: Click 🗑️ (Delete) icon - blinks for confirmation

### Getting Recommendations

1. **Go to "Advisor" tab**

2. **Describe your purchase**:
   - "Buying groceries at BigBasket for ₹5,000"
   - "Paying LIC premium ₹20,000 online"
   - "Shopping on Amazon for ₹3,000"

3. **Click "Get Best Card Suggestion"**

4. **AI analyzes** your card portfolio and returns:
   - Best card to use
   - Expected reward amount
   - Calculation explanation
   - Alternative cards (if close)

### Understanding Usage Stats

After each AI request, a toast notification appears at the bottom:

```
✓ 1 request • 2,450 tokens
  Prompt: 1,200 • Response: 1,250
```

- **Requests**: Number of API calls (includes retries)
- **Tokens**: API usage (affects billing)
- **Auto-dismisses**: After 3 seconds

---

## 🔧 Configuration

### Capacitor Config

`capacitor.config.json`:

```json
{
  "appId": "com.mycompany.cardadvisor",
  "appName": "Card Advisor AI",
  "webDir": "www",
  "server": {
    "androidScheme": "https"
  }
}
```

### API Configuration

- **Model**: `gemini-2.5-flash-preview-09-2025`
- **Tools**: Google Search (for real-time bank data)
- **Rate Limiting**: Automatic retry with exponential backoff
- **Max Retries**: 4 attempts

### Storage

- **Type**: localStorage (WebView)
- **Key**: `cardAdvisorCards`
- **Format**: JSON array of card objects
- **Persistence**: Survives app restarts

---

## 🎨 Features Deep Dive

### 1. AI-Powered Card Rule Extraction

**How it works:**
- Searches official bank websites (HDFC, SBI, ICICI, Axis, etc.)
- Extracts reward rates, bonus categories, exclusions
- Formats as mobile-friendly bullet points
- Caches locally for offline access

**Example Output:**
```
### Reward Structure
- Base Rate: 1 RP per ₹150
- Bonus: 5% on Amazon, Swiggy
- Exclusions: Rent, insurance, fuel

### Redemption
- 1 RP = ₹0.25
```

### 2. Intelligent Recommendation Engine

**Algorithm:**
- Parses all saved card rules
- Matches purchase category with MCC codes
- Calculates effective reward rates
- Considers accelerated categories
- Accounts for exclusions
- Returns best card with calculation

**Example:**
```
Input: "Buying ₹5,000 groceries at BigBasket"
Output: 
✅ Use HDFC Millennia
💰 Earn ₹250 (5% cashback)
📊 Effective rate: 5% (accelerated category)
```

### 3. Real-Time Data Fetching

Uses Google Search tool in Gemini API:
- Searches: `"HDFC Millennia reward rules site:hdfcbank.com"`
- Verifies from official T&C pages
- Updates automatically when banks change rules

### 4. LaTeX & Formatting Cleanup

Automatic conversion:
- `$\times$` → `×`
- `\text{value}` → `value`
- `$100` → `₹100`
- Tables → Mobile-friendly cards
- Markdown → Styled HTML

### 5. Error Handling & Retry Logic

- **Rate Limiting**: Exponential backoff (1s, 2s, 4s, 8s)
- **Network Errors**: Automatic retry
- **Invalid Responses**: User-friendly error messages
- **Validation**: API key format check

---

## 🎨 UI/UX Features

### Tabbed Interface

- **Advisor Tab**: Main recommendation engine (default)
- **My Cards Tab**: Card management with badge count

### Responsive Design

- Optimized for Samsung S24 (6.2" AMOLED)
- Edge-to-edge display
- Dark status bar icons (light background)
- Safe area insets for notch/camera

### Visual Elements

- **Header**: Left-aligned with app icon and status
- **Cards**: Gradient backgrounds, shadow effects
- **Buttons**: Smooth hover animations
- **Icons**: Indigo refresh 🔄, Red delete 🗑️
- **Animations**: Blink on delete, fade notifications

### Accessibility

- Readable fonts (Inter family)
- High contrast colors
- Touch-optimized button sizes (py-4 = 16px vertical padding)
- Clear error messages

---

## 🔒 Security & Privacy

### Data Storage

- ✅ All card data stored **locally** (no cloud sync)
- ✅ API key stored in **localStorage** (device only)
- ✅ No user authentication required
- ✅ No personal data collected
- ✅ No analytics or tracking

### API Key Security

- Masked input field (type="password")
- Never logged or transmitted (except to Gemini API)
- User-controlled (can be changed anytime)
- Stored per-device

### Permissions

Required Android permissions:
- `INTERNET` - For API calls only

No other permissions requested!

---

## 📊 Performance

### App Size

- APK: ~5-10 MB (debug build)
- Installed: ~15-20 MB

### API Usage

Typical token consumption:
- Fetch Card Rules: ~1,500-3,000 tokens
- Get Recommendation: ~2,000-4,000 tokens
- Refresh Rules: ~1,500-2,500 tokens

### Response Times

- Card lookup: 3-6 seconds
- Recommendation: 2-5 seconds
- Depends on API latency and search complexity

---

## 🛠️ Development Workflow

### Making Changes

1. **Edit** `www/index.html`

2. **Copy to Android**:
   ```bash
   npx cap copy android
   ```

3. **Rebuild** in Android Studio

4. **Test** on device/emulator

### Debug Mode

- Check Chrome DevTools: `chrome://inspect`
- View console logs from WebView
- Inspect localStorage

### Clean Build

```bash
cd android
./gradlew clean
./gradlew assembleDebug
```

---

## 🐛 Troubleshooting

### Common Issues

**1. "Default activity not found"**
- Solution: Open `android` folder, not root folder

**2. Empty/blank page**
- Run: `npx cap copy android`
- Rebuild project

**3. API key not working**
- Verify key starts with `AIza`
- Check key has Gemini API enabled
- Test at [AI Studio](https://aistudio.google.com)

**4. "Rate limit" errors**
- Wait a few seconds
- App automatically retries
- Check API quota

**5. Status bar icons white on white**
- Already fixed! Dark icons enabled for light background

---

## 📝 Version History

### Current Version (v1.0)

**Features:**
- ✅ AI-powered card recommendations
- ✅ Real-time bank website data
- ✅ localStorage persistence
- ✅ Tabbed interface
- ✅ Usage analytics
- ✅ Configurable API key
- ✅ LaTeX cleanup
- ✅ Request count tracking
- ✅ Bottom toast notifications

**Optimizations:**
- Mobile-friendly markdown rendering
- Table-to-card conversion
- Dark status bar icons
- Full screen S24 support
- Indigo refresh, red delete icons
- Delete confirmation blink

---

## 🚀 Future Enhancements

Potential improvements:
- [ ] Firebase sync (optional cloud backup)
- [ ] Multiple users/profiles
- [ ] Card comparison view
- [ ] Spending analytics
- [ ] Transaction history
- [ ] Expense categorization
- [ ] Push notifications for offers
- [ ] Widget for quick recommendations

---

## 🤝 Contributing

This is a personal project. Feel free to:
- Fork and modify for your needs
- Report issues
- Suggest improvements

---

## 📄 License

MIT License - Free to use and modify

---

## 🙏 Acknowledgments

- **Google Gemini** - AI engine
- **Capacitor** - Web-to-native framework
- **Tailwind CSS** - Styling framework
- **Android Studio** - Development environment

---

## 📧 Support

For issues or questions:
- Check the troubleshooting section
- Review console logs (`chrome://inspect`)
- Verify API key configuration

---

## 🎓 Learn More

- [Capacitor Documentation](https://capacitorjs.com/docs)
- [Gemini API Docs](https://ai.google.dev/docs)
- [Android Development](https://developer.android.com)
- [Tailwind CSS](https://tailwindcss.com)

---

**Built with ❤️ for Indian credit card users**

*Maximize your rewards, minimize the guesswork!* 💳✨

