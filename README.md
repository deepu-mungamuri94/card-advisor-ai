# 💳 Card Advisor AI

> **Maximize every spend** - An intelligent Android app that analyzes your credit card portfolio and suggests the optimal card for each purchase using Google's Gemini AI.

[![Android](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com/)
[![Capacitor](https://img.shields.io/badge/Framework-Capacitor-blue.svg)](https://capacitorjs.com/)
[![Gemini AI](https://img.shields.io/badge/AI-Google%20Gemini-orange.svg)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📱 Overview

**Card Advisor AI** is a mobile-first application that leverages **Google's Gemini 2.5 Flash AI** with **Google Search** to provide intelligent, real-time credit card recommendations. It automatically fetches comprehensive reward rules from official bank websites across **70+ spending categories** and helps you maximize cashback and reward points on every purchase.

### 🌟 Key Features

#### 🤖 AI-Powered Intelligence
- **Real-Time Data**: Fetches latest rules from official bank websites
- **Google Search Integration**: Verifies information from bank T&C pages
- **70+ Categories Covered**: Healthcare, Groceries, Fuel, Dining, Entertainment, Travel, Shopping, Utilities, Insurance, Education, and more
- **Comprehensive Analysis**: Includes movie tickets (BookMyShow 1+1), OTT subscriptions, lounge access, and all benefits

#### 💼 Smart Card Management
- **Card Icon Display**: Each card shows with a beautiful credit card icon
- **Scrollable Modal View**: Full-screen modal to view complete card rules
- **In-Modal Reload**: Refresh rules without leaving the detail view
- **Quick Actions**: View (👁️), Reload (🔄), Edit (✏️), Delete (🗑️)
- **Offline Storage**: All cards stored locally using localStorage

#### 🎨 Modern Design
- **Beautiful UI**: Glass morphism effects with gradient accents
- **Full-Screen**: Edge-to-edge display with safe area support
- **Status Bar Compatible**: Content properly positioned below mobile status bar
- **Hamburger Menu**: Clean navigation with branded header
- **Responsive**: Optimized for all Android devices (tested on Samsung S24)

#### 🇮🇳 India-Focused
- **Indian Currency**: All amounts in ₹ (Rupees)
- **Indian Banks**: HDFC, SBI, ICICI, Axis, etc.
- **Indian Platforms**: BookMyShow, Swiggy, Zomato, BigBasket, etc.
- **Local Categories**: Kirana stores, IRCTC, DTH recharge, and more

#### 📊 Usage Transparency
- **Token Tracking**: See exact API usage (prompt, response, total tokens)
- **Request Count**: Track number of AI requests
- **Toast Notifications**: Auto-dismissing usage stats after each request

#### 🔒 Privacy-First
- **No Cloud**: All data stored locally on device
- **No Sign-Up**: No authentication required
- **No Tracking**: Zero analytics or data collection
- **API Key Control**: You manage your own Gemini API key

---

## 🚀 Quick Start

### Prerequisites

- **Android Studio** (Narwhal 2025.1.2 or later)
- **Node.js** (v16+)
- **Google Gemini API Key** → [Get free key](https://aistudio.google.com/app/apikey)

### Installation (5 Minutes)

```bash
# 1. Navigate to project
cd /Users/dmungamuri/AndroidStudioProjects/cardadvisorapp

# 2. Copy web assets to Android
npx cap copy android

# 3. Open Android project in Android Studio
open -a "Android Studio" ./android

# 4. Build APK: Build → Build APK(s)
# APK location: android/app/build/outputs/apk/debug/app-debug.apk

# 5. Install on device via USB or Google Drive
```

**📖 Detailed setup guide**: See [QUICKSTART.md](QUICKSTART.md)

---

## 🎯 How to Use

### 1️⃣ Configure API Key (One-Time Setup)

1. Open the app
2. Click **hamburger menu** (☰) → **Settings**
3. Get your free API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
4. Paste and save (stored locally, never shared)

### 2️⃣ Add Your Credit Cards

1. **Open menu** → **My Cards**
2. **Enter exact card name**:
   - Example: "HDFC Millennia Credit Card"
   - Example: "SBI Cashback Credit Card"
   - Example: "ICICI Amazon Pay Credit Card"
3. **Click "Fetch & Save Card Rules"**
4. **AI fetches comprehensive rules** (takes 3-8 seconds):
   - Base reward rates
   - Accelerated categories (groceries, fuel, dining, etc.)
   - Entertainment offers (movie tickets, OTT)
   - Travel benefits (lounge, insurance, cabs)
   - Shopping offers (online/offline)
   - Utility rewards
   - Exclusions (rent, insurance premiums)
   - Redemption value
   - Annual fee waivers
   - Welcome bonuses

### 3️⃣ View Card Details

- **Click the purple eye icon** (👁️) on any card
- **Scrollable modal** opens with full rules
- **Reload button** in modal to fetch latest rules
- **Close button** or tap outside to dismiss

### 4️⃣ Get Smart Recommendations

1. **Open menu** → **AI Advisor**
2. **Describe your purchase**:
   - "Buying ₹5,000 groceries at BigBasket"
   - "Booking ₹15,000 flight on MakeMyTrip"
   - "Paying ₹3,000 electricity bill"
   - "Shopping ₹2,000 on Amazon"
3. **AI analyzes** your entire card portfolio
4. **Get recommendation** with:
   - Best card to use
   - Expected reward amount
   - Calculation breakdown
   - Alternative cards (if close)

### 5️⃣ Keep Rules Updated

- **Manual refresh**: Click 🔄 icon on card list
- **In-modal refresh**: Click "Reload Rules" in detail view
- **AI re-fetches** from official bank website

---

## 📋 Comprehensive Coverage

### 🏥 Healthcare & Medical
- Pharmacies (Apollo, Netmeds, 1mg)
- Hospitals & clinics
- Health insurance premiums
- Diagnostic tests

### 🛒 Groceries & Supermarkets
- Physical stores (BigBasket, D-Mart, Reliance Fresh)
- Online grocery (Grofers, Swiggy Instamart, Blinkit)
- Kirana stores

### ⛽ Fuel & Transportation
- Petrol/Diesel (BPCL, HPCL, Indian Oil, Shell)
- Fuel surcharge waivers
- EV charging
- Metro/Train recharge
- Toll payments

### 🍽️ Dining & Food
- Restaurants (fine dining, casual, QSR)
- Food delivery (Swiggy, Zomato)
- Cafes (Starbucks, CCD)
- Dining memberships (Zomato Gold)

### 🎬 Entertainment
- **Movie tickets** (BookMyShow 1+1 offers, PVR, INOX)
- **OTT subscriptions** (Netflix, Prime, Disney+, Hotstar)
- Concert tickets
- Amusement parks

### ✈️ Travel
- **Flights** (domestic/international)
- **Hotels** (MakeMyTrip, Goibibo, OYO)
- **Airport lounges** (domestic/international access)
- **Travel insurance**
- **Cabs** (Uber, Ola)
- **Railways** (IRCTC)
- **Forex charges**

### 🛍️ Shopping
- **Online**: Amazon, Flipkart, Myntra, Ajio, Nykaa
- **Offline**: Malls, electronics stores, fashion outlets
- **Categories**: Electronics, fashion, jewelry, furniture

### 💡 Utilities & Bills
- Electricity, water, gas bills
- Broadband, mobile recharge
- DTH & cable TV
- Postpaid bills

### 🛡️ Insurance & Education
- Life, health, vehicle insurance premiums
- School/college fees
- Coaching, online courses

### 💆 Lifestyle & Wellness
- Gym memberships
- Spa & salon
- Golf courses
- Yoga centers

---

## 🏗️ Architecture

### Technology Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | HTML5, Vanilla JavaScript, Tailwind CSS |
| **Mobile Runtime** | Capacitor 6.x (Web-to-Native) |
| **Platform** | Android Native |
| **AI Engine** | Google Gemini 2.5 Flash with Google Search |
| **Storage** | localStorage (WebView API) |
| **Build System** | Gradle, Android Studio |

### Project Structure

```
cardadvisorapp/
├── android/                      # Native Android project
│   ├── app/
│   │   ├── src/main/
│   │   │   ├── assets/public/    # Auto-copied web assets
│   │   │   ├── java/             # MainActivity.java
│   │   │   └── res/              # Android resources, icons
│   │   └── build.gradle
│   └── build.gradle
├── www/                          # Web application source
│   ├── index.html                # Single-file app (~1650 lines)
│   └── (copied to android assets)
├── capacitor.config.json         # Capacitor configuration
├── package.json                  # Node dependencies
├── README.md                     # This file
├── QUICKSTART.md                 # Detailed setup guide
└── ARCHITECTURE.md               # Technical architecture
```

### Key Design Decisions

1. **Single HTML File**: Entire app in one file for simplicity and WebView compatibility
2. **No External JS**: All JavaScript inline to avoid module loading issues
3. **localStorage**: Simple, reliable persistence without backend
4. **Capacitor**: Modern web-to-native bridge (better than Cordova)
5. **Tailwind CDN**: Quick styling without build process
6. **Gemini with Search**: Real-time data from official sources

**📖 Detailed architecture**: See [ARCHITECTURE.md](ARCHITECTURE.md)

---

## 🎨 UI/UX Highlights

### Navigation
- **Hamburger menu** (☰) for main navigation
- **AI Advisor** - Default landing screen
- **My Cards** - Card management with count badge
- **Settings** - API key configuration

### Card List Design
- **💳 Credit card icon** prefix on each card
- **Card name** with edit button
- **Quick action buttons**:
  - 👁️ **View** (purple) - Open full rules modal
  - 🔄 **Reload** (indigo) - Refresh from bank website
  - 🗑️ **Delete** (red) - Remove card with blink animation

### Modal View
- **Full-screen scrollable** modal for card rules
- **Gradient header** with card icon and name
- **Formatted content** with markdown rendering
- **Footer actions**:
  - "Reload Rules" button (left)
  - "Close" button (right)
- **Click outside** to dismiss

### Visual Polish
- **Subtle gradient background** (8% opacity for content focus)
- **Glass morphism** effects on cards
- **Smooth animations** on interactions
- **Shadow depth** for visual hierarchy
- **Responsive touch targets** (minimum 44x44px)

### Mobile Optimizations
- **Safe area support**: Content below status bar (notch/camera)
- **Full-screen display**: Edge-to-edge with proper spacing
- **Dark status icons**: Visible on light background
- **Optimized scrolling**: Smooth performance
- **Touch-friendly**: Large tap targets, clear visual feedback

---

## 🔒 Security & Privacy

### Data Storage
- ✅ **100% Local**: All cards stored on device only
- ✅ **No Cloud Sync**: Zero data transmission (except AI API)
- ✅ **No Account**: No sign-up, login, or user data
- ✅ **No Analytics**: Zero tracking or telemetry
- ✅ **No Permissions**: Only INTERNET for API calls

### API Key Management
- ✅ **User-Controlled**: You provide your own API key
- ✅ **Masked Input**: Never displayed (type="password")
- ✅ **Local Storage**: Saved in device localStorage
- ✅ **No Sharing**: Key never sent anywhere except Gemini API
- ✅ **Free Tier**: Gemini has generous free quota

### Transparency
- ✅ **Open Source**: All code visible in repository
- ✅ **Token Usage**: See exact API consumption
- ✅ **Request Count**: Track number of calls
- ✅ **No Hidden Costs**: You control API key and usage

---

## 📊 Performance

### App Metrics
- **APK Size**: ~5-8 MB (debug), ~3-5 MB (release)
- **Installed Size**: ~15-20 MB
- **Memory Usage**: ~50-80 MB RAM
- **Battery Impact**: Minimal (only during AI requests)

### API Usage (Typical)
- **Fetch Card Rules**: 2,000-5,000 tokens (~4-8 seconds)
- **Get Recommendation**: 2,500-6,000 tokens (~3-6 seconds)
- **Refresh Rules**: 2,000-4,500 tokens (~4-7 seconds)

### Gemini Free Tier
- **Quota**: 1,500 requests/day (very generous!)
- **Rate Limit**: 15 requests/minute
- **Token Limit**: 1 million tokens/minute
- **Cost**: $0 (completely free)

### Optimization Features
- ✅ **Automatic Retry**: Exponential backoff for rate limits
- ✅ **Request Throttling**: Prevents rapid-fire calls
- ✅ **Response Caching**: Rules stored locally
- ✅ **Efficient Parsing**: Minimal processing overhead

---

## 🛠️ Development

### Making Changes

```bash
# 1. Edit web content
code www/index.html

# 2. Copy to Android
npx cap copy android

# 3. Rebuild in Android Studio
# Build → Build APK(s)

# 4. Test on device
```

### Debug Tips

#### Chrome DevTools (WebView Debugging)
```bash
# 1. Enable USB debugging on phone
# 2. Connect via USB
# 3. Open Chrome: chrome://inspect
# 4. Click "inspect" under your app
# 5. Access console, network, storage tabs
```

#### View localStorage
```javascript
// In Chrome DevTools console:
localStorage.getItem('cardAdvisorCards');
localStorage.getItem('geminiApiKey');
```

#### Clear All Data
```javascript
// In Chrome DevTools console:
localStorage.clear();
location.reload();
```

### Clean Build
```bash
cd android
./gradlew clean
./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 🐛 Troubleshooting

### Common Issues & Solutions

#### ❌ "Default activity not found"
**Cause**: Opening root folder instead of `android` folder  
**Fix**: Open `/path/to/cardadvisorapp/android` in Android Studio

#### ❌ Blank white screen
**Cause**: Web assets not copied to Android  
**Fix**: Run `npx cap copy android` and rebuild

#### ❌ API key not working
**Solutions**:
- Verify key starts with `AIza`
- Check Gemini API is enabled at [Google AI Studio](https://aistudio.google.com)
- Try key in browser first
- Clear cache: Settings → Clear data

#### ❌ "Rate limit exceeded" (429 error)
**Solutions**:
- Wait 60 seconds (automatic retry)
- Check your usage at Google AI Studio
- Ensure not exceeding 15 requests/minute

#### ❌ Status bar collision
**Already fixed!** Safe area insets applied to header and menu.

#### ❌ Rules not showing movie/dining offers
**Already fixed!** AI now explicitly fetches 70+ categories including entertainment and dining.

#### ❌ Modal reload not working
**Already fixed!** Modal now uses same reload function as list view.

---

## 📝 Version History

### v1.1 (Current) - Comprehensive Update
**Release Date**: January 2025

**New Features**:
- ✅ Card icon prefix on all cards
- ✅ Scrollable full-screen modal for rules
- ✅ In-modal reload functionality
- ✅ Comprehensive AI prompts (70+ categories)
- ✅ Healthcare/Medical category
- ✅ Grocery rewards detailed
- ✅ Fuel surcharge tracking
- ✅ Entertainment (BookMyShow, OTT)
- ✅ Travel (flights, hotels, lounge, cabs)
- ✅ Utilities & bills
- ✅ Insurance & education
- ✅ Lifestyle & wellness

**UI Improvements**:
- ✅ Lighter background (92% reduced opacity)
- ✅ Safe area support for status bar
- ✅ Menu properly positioned below status bar
- ✅ Full-screen edge-to-edge display
- ✅ Hamburger menu navigation
- ✅ Glass morphism effects
- ✅ Smooth animations

**Technical**:
- ✅ Enhanced AI prompt engineering
- ✅ 15 major spending categories
- ✅ 70+ subcategories
- ✅ 100+ platform/brand names
- ✅ Explicit completeness rules
- ✅ No truncation instructions
- ✅ Modal reload reuses existing function

### v1.0 - Initial Release
**Release Date**: December 2024

- ✅ AI-powered recommendations
- ✅ Real-time bank website data
- ✅ localStorage persistence
- ✅ Tabbed interface
- ✅ Usage analytics
- ✅ Configurable API key
- ✅ Token tracking
- ✅ Toast notifications

---

## 🚀 Roadmap

### Planned Features (Future)
- [ ] **Spending Analytics**: Track transactions and visualize spending
- [ ] **Billing Cycle**: Set card billing cycles for better recommendations
- [ ] **SMS Parsing**: Auto-extract transactions from bank SMS
- [ ] **Cap Tracking**: Track monthly/quarterly caps
- [ ] **Card Comparison**: Side-by-side comparison view
- [ ] **Export/Import**: Backup and restore card data
- [ ] **Dark Mode**: Theme toggle for night usage
- [ ] **Widgets**: Home screen widget for quick recommendations
- [ ] **Notifications**: Alerts for expiring offers

### Under Consideration
- [ ] Firebase sync (optional cloud backup)
- [ ] Multiple profiles
- [ ] iOS version (Capacitor supports it!)
- [ ] Browser extension
- [ ] Perplexity AI integration (alternative to Gemini)

---

## 🤝 Contributing

This is a personal project, but contributions are welcome!

### Ways to Contribute
- 🐛 **Report Bugs**: Open issues with details
- 💡 **Suggest Features**: Share your ideas
- 📝 **Improve Docs**: Fix typos, add clarity
- 🔧 **Submit PRs**: Bug fixes and enhancements

### Development Setup
```bash
# Fork the repo
git clone https://github.com/deepu-mungamuri94/card-advisor-ai.git
cd card-advisor-ai

# Make changes to www/index.html

# Test
npx cap copy android
# Open android/ in Android Studio, build & run

# Commit
git add .
git commit -m "Your message"
git push origin your-branch
# Create Pull Request
```

---

## 📄 License

**MIT License** - Free to use, modify, and distribute

```
Copyright (c) 2025 Deepu Mungamuri

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 🙏 Acknowledgments

### Technologies
- **[Google Gemini](https://ai.google.dev/)** - Powerful AI engine
- **[Capacitor](https://capacitorjs.com/)** - Modern web-to-native framework
- **[Tailwind CSS](https://tailwindcss.com/)** - Utility-first CSS framework
- **[Android Studio](https://developer.android.com/studio)** - Development environment

### Inspiration
- Indian credit card users who want to maximize rewards
- Personal need for smart card recommendations
- Desire for privacy-first, local-storage solutions

---

## 📧 Support

### Getting Help
1. **Check Documentation**:
   - [QUICKSTART.md](QUICKSTART.md) - Setup guide
   - [ARCHITECTURE.md](ARCHITECTURE.md) - Technical details
   - This README - Feature overview

2. **Debug Tools**:
   - Chrome DevTools: `chrome://inspect`
   - Android Logcat: View → Tool Windows → Logcat
   - Console logs in WebView

3. **Common Issues**: See [Troubleshooting](#-troubleshooting) section

### Contact
- **GitHub Issues**: [Report bugs or request features](https://github.com/deepu-mungamuri94/card-advisor-ai/issues)
- **Repository**: [View source code](https://github.com/deepu-mungamuri94/card-advisor-ai)

---

## 🎓 Learn More

### Documentation
- [Capacitor Docs](https://capacitorjs.com/docs) - Mobile framework
- [Gemini API](https://ai.google.dev/docs) - AI integration
- [Android Dev](https://developer.android.com) - Platform guides
- [Tailwind CSS](https://tailwindcss.com/docs) - Styling

### Useful Resources
- [Gemini API Pricing](https://ai.google.dev/pricing) - Always free tier info
- [Capacitor Plugins](https://capacitorjs.com/docs/plugins) - Native capabilities
- [Android WebView](https://developer.android.com/guide/webapps/webview) - How it works

---

## 🌟 Star This Project

If you find this useful, please ⭐ star the repository!

---

**Built with ❤️ for Indian credit card users**

*Make every spend rewarding!* 💳✨

