# 🏗️ Technical Architecture - Card Advisor AI

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    Card Advisor AI (Android)                 │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Capacitor WebView                      │    │
│  │  ┌─────────────────────────────────────────────┐   │    │
│  │  │          Web Application Layer              │   │    │
│  │  │  - index.html (1169 lines)                  │   │    │
│  │  │  - JavaScript (ES6+)                        │   │    │
│  │  │  - Tailwind CSS                             │   │    │
│  │  └─────────────────────────────────────────────┘   │    │
│  │                      ↕                               │    │
│  │  ┌─────────────────────────────────────────────┐   │    │
│  │  │          Browser APIs                       │   │    │
│  │  │  - localStorage (data persistence)          │   │    │
│  │  │  - fetch (HTTP requests)                    │   │    │
│  │  └─────────────────────────────────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                      ↕                                        │
│  ┌─────────────────────────────────────────────────────┐    │
│  │          Native Android Bridge                      │    │
│  │  - MainActivity.java (BridgeActivity)              │    │
│  │  - WebView with JS Bridge                          │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                      ↕
┌─────────────────────────────────────────────────────────────┐
│              External Services (Cloud)                       │
├─────────────────────────────────────────────────────────────┤
│  - Google Gemini 2.5 Flash API (AI Engine)                 │
│  - Google Search Tool (Bank website data)                   │
└─────────────────────────────────────────────────────────────┘
```

---

## Core Components

### 1. Web Application (`www/index.html`)

**Single-file architecture** with three main sections:

#### A. UI Layer (HTML)
```html
<!-- Header with App Icon -->
<header> ... </header>

<!-- Tab Navigation -->
<div id="tabs">
  - Advisor Tab (default)
  - My Cards Tab (with badge)
</div>

<!-- Advisor Tab Content -->
<section id="advisor-tab-content">
  - Purchase query input
  - Get recommendation button
  - Results display
  - Loading indicator
</section>

<!-- My Cards Tab Content -->
<section id="cards-tab-content">
  - Add card form
  - Card portfolio list
  - Card management (edit, refresh, delete)
</section>

<!-- Modals -->
- Settings modal (API key)
- Rename card modal

<!-- Toast Notification -->
<div id="usage-toast"> ... </div>
```

#### B. Business Logic (JavaScript)

**Data Management:**
```javascript
// Card storage
let cardList = [];
let userId = 'local-user';

// Load from localStorage
function loadCardsFromStorage() { ... }

// Save to localStorage
function saveCardsToStorage() { ... }
```

**API Communication:**
```javascript
// Main API function
async function fetchGeminiResponse(systemPrompt, userQuery) {
  - Retry logic (max 4 attempts)
  - Rate limit handling (exponential backoff)
  - Token usage tracking
  - Request count tracking
  return { text, usage }
}
```

**Key Functions:**

| Function | Purpose | API Calls |
|----------|---------|-----------|
| `fetchAndSaveCardRules()` | Add new card | 1 |
| `refreshCardRules()` | Update card rules | 1 |
| `generateSuggestion()` | Get recommendation | 1 |
| `markdownToHtml()` | Format AI response | 0 |
| `displayUsageStats()` | Show usage toast | 0 |

#### C. Styling (Tailwind + Custom CSS)

**Tailwind Utilities:**
- Responsive grid system
- Color scheme (indigo primary, gray base)
- Shadow effects (`shadow-md`, `shadow-lg`)
- Animations (`animate-spin`, `transition`)

**Custom CSS:**
```css
/* LaTeX cleanup handled via JavaScript */
/* Markdown rendering with styled lists/tables */
/* Blink animation for delete confirmation */
@keyframes blink-red { ... }
```

---

## Data Flow

### Flow 1: Adding a Card

```
User Input (Card Name)
    ↓
fetchAndSaveCardRules()
    ↓
Construct AI Prompt:
  - System: "Search official bank website..."
  - User: "Find rules for [Card Name]"
    ↓
fetchGeminiResponse()
    ↓
API Request to Gemini
    ↓
[Gemini uses Google Search Tool]
    ↓
Search bank websites (HDFC, SBI, etc.)
    ↓
Extract reward rules, exclusions
    ↓
Return structured markdown
    ↓
Clean LaTeX artifacts
    ↓
Save to cardList array
    ↓
saveCardsToStorage() → localStorage
    ↓
renderCards() → Display in UI
    ↓
displayUsageStats() → Show toast
```

### Flow 2: Getting Recommendation

```
User Input (Purchase Description)
    ↓
generateSuggestion()
    ↓
Gather all card rules from cardList
    ↓
Construct AI Prompt:
  - System: "Analyze cards and recommend best..."
  - User: "Purchase: [Description]"
  - Context: Full card portfolio
    ↓
fetchGeminiResponse()
    ↓
AI analyzes:
  - Purchase category
  - MCC codes
  - Card reward rates
  - Exclusions
    ↓
Calculate effective rates
    ↓
Return recommendation with calculation
    ↓
markdownToHtml() → Format
    ↓
Display in results section
    ↓
displayUsageStats() → Show toast
```

---

## AI Prompt Engineering

### Card Rules Extraction Prompt

**System Prompt:**
```
You are a financial information specialist with access to real-time web search.

Task:
1. Search OFFICIAL BANK WEBSITE for "[Card Name]"
2. Verify from bank's reward program T&C
3. Provide MOBILE-FRIENDLY summary using BULLET POINTS

Required Information:
- Reward Point earning rate (per ₹100/₹150)
- Accelerated/Bonus categories
- Key Exclusions
- Redemption value

Formatting Rules:
- Simple bullet points, NO tables
- Use bold (**text**) for emphasis
- Keep lines short for mobile
- NO LaTeX formatting
- Currency in Rupees (₹) ONLY
```

**User Prompt:**
```
Search the official bank website for "[Card Name]" credit card 
(INDIAN market) and provide current reward rules in RUPEES (₹). 
Format as simple bullet points for mobile. NO TABLES. NO LATEX.
```

### Recommendation Prompt

**System Prompt:**
```
You are a world-class financial analyst for INDIAN market.

Analyze: Provided INDIAN credit cards
Identify: SINGLE best card for purchase
Explain: Maximum reward/cashback value
Compare: Second-best option if close

Formatting Rules:
- Bullet points, NO tables
- Bold card names, amounts
- Short, scannable lines
- Section headings (### Best Card)
- Show calculations: "5% of ₹1000 = ₹50"
- Use emojis sparingly (✅, 💰, 🎯)

Currency Rules:
- ALL amounts in Rupees (₹) ONLY
- NEVER use $ or dollars

Card Portfolio:
[Full card data here]
```

**User Prompt:**
```
I am planning to make the following purchase in INDIA: "[Purchase]"
Which card should I use to maximize rewards? 
State calculation clearly in RUPEES (₹). 
FORMAT FOR MOBILE - NO TABLES. NO LATEX.
```

---

## Storage Schema

### localStorage Key: `cardAdvisorCards`

**Value:** JSON array of card objects

**Card Object Structure:**
```javascript
{
  id: string,          // e.g., "hdfc_millennia" (generated)
  name: string,        // e.g., "HDFC Millennia"
  rules: string        // Markdown-formatted rules from AI
}
```

**Example:**
```json
[
  {
    "id": "hdfc_millennia",
    "name": "HDFC Millennia",
    "rules": "### Reward Structure\n- Base: 1% cashback\n- Amazon: 5% cashback..."
  },
  {
    "id": "sbi_pulse",
    "name": "SBI Pulse",
    "rules": "### Earning Rate\n- 10 RP per ₹100..."
  }
]
```

### localStorage Key: `gemini_api_key`

**Value:** String (encrypted by WebView)

---

## Error Handling Strategy

### 1. Network Errors

```javascript
try {
  const response = await fetch(apiUrl, { ... });
} catch (error) {
  console.error("Network error:", error);
  showNotification("Connection failed. Retrying...", true);
  // Retry with exponential backoff
}
```

### 2. API Rate Limiting

```javascript
if (response.status === 429) {
  const delay = Math.pow(2, attempt) * 1000;
  showNotification(`Rate limited. Retrying in ${delay/1000}s...`, true);
  await new Promise(resolve => setTimeout(resolve, delay));
  attempt++;
  continue; // Retry
}
```

### 3. Invalid Responses

```javascript
if (!text || text.length < 50) {
  console.warn('Response too short:', text);
  lastError = 'Response too short or invalid';
  // Try again up to maxRetries
}
```

### 4. User Errors

```javascript
if (!cardName.trim()) {
  showNotification("Please enter card name", true);
  return; // Early exit
}

if (!isApiKeyConfigured()) {
  showNotification("⚙️ Please configure API key first", true);
  setTimeout(() => openSettingsModal(), 500);
  return;
}
```

---

## Performance Optimizations

### 1. Lazy Loading

- Cards rendered only when "My Cards" tab is active
- AI results rendered only after API response

### 2. Caching

- Card rules cached in localStorage
- No API calls on app restart (data persists)

### 3. Efficient Rendering

```javascript
// Single innerHTML update vs multiple DOM manipulations
container.innerHTML = cardList.map(card => `...`).join('');
```

### 4. Debouncing (Future)

Could add for search/filter:
```javascript
const debounce = (fn, delay) => {
  let timeoutId;
  return (...args) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn(...args), delay);
  };
};
```

---

## Security Measures

### 1. API Key Protection

- Stored in localStorage (sandboxed per-app)
- Masked input field (`type="password"`)
- Never logged or exposed in UI
- User-controlled (no default key)

### 2. Input Sanitization

```javascript
// Card name sanitization
const cardId = cardName.replace(/[^a-zA-Z0-9]/g, '_').toLowerCase();

// HTML escaping in markdown
html = html.replace(/<script>/gi, '&lt;script&gt;');
```

### 3. HTTPS Only

```json
// capacitor.config.json
{
  "server": {
    "androidScheme": "https"  // Forces HTTPS for WebView
  }
}
```

### 4. Minimal Permissions

AndroidManifest.xml:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<!-- No other permissions requested -->
```

---

## Testing Strategy

### Manual Testing Checklist

- [ ] Add card with valid name
- [ ] Add card with special characters
- [ ] Refresh card rules
- [ ] Delete card (check blink animation)
- [ ] Rename card
- [ ] Get recommendation with 0 cards (should warn)
- [ ] Get recommendation with 1 card
- [ ] Get recommendation with multiple cards
- [ ] Test with invalid API key
- [ ] Test with no API key
- [ ] Test rate limiting (make many requests)
- [ ] Test offline mode (should fail gracefully)
- [ ] Test localStorage persistence (restart app)
- [ ] Test on different screen sizes

### Chrome DevTools Testing

```bash
# Connect device via USB
adb devices

# Open Chrome DevTools
chrome://inspect

# Select "Card Advisor AI"
# Console tab: View JavaScript logs
# Application tab: Check localStorage
# Network tab: Monitor API calls
```

---

## Build Process

### 1. Web → Android Asset Copy

```bash
npx cap copy android
```

**What happens:**
```
www/index.html → android/app/src/main/assets/public/index.html
www/**        → android/app/src/main/assets/public/**
capacitor.config.json → android/app/src/main/assets/
```

### 2. Android Build

```bash
cd android
./gradlew assembleDebug
```

**Gradle tasks:**
1. `preBuild` - Check dependencies
2. `compileDebugJavaWithJavac` - Compile Java
3. `mergeDebugResources` - Merge resources
4. `processDebugManifest` - Process manifest
5. `packageDebug` - Create APK
6. `assembleDebug` - Final assembly

**Output:** `android/app/build/outputs/apk/debug/app-debug.apk`

### 3. APK Structure

```
app-debug.apk
├── AndroidManifest.xml
├── classes.dex            # Compiled Java
├── resources.arsc         # Binary resources
├── assets/
│   └── public/
│       └── index.html     # Your web app
└── lib/
    └── arm64-v8a/         # Native libraries
```

---

## Future Architecture Improvements

### 1. Code Splitting

Split `index.html` into modules:
```
www/
├── index.html
├── js/
│   ├── api.js          # Gemini API calls
│   ├── storage.js      # localStorage logic
│   ├── ui.js           # Rendering functions
│   └── utils.js        # Helpers
└── css/
    └── styles.css      # Custom CSS
```

### 2. State Management

Implement reactive state:
```javascript
const state = {
  cards: [],
  apiKey: '',
  usage: {}
};

// Reactive updates
const setState = (updates) => {
  Object.assign(state, updates);
  render(); // Re-render UI
};
```

### 3. Service Worker

Add offline capabilities:
```javascript
// sw.js
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
  );
});
```

### 4. Firebase Integration (Optional)

```
Firebase
├── Authentication (Email/Google)
├── Firestore (Cloud sync)
├── Analytics (Usage tracking)
└── Remote Config (Feature flags)
```

---

## Dependencies

### Runtime Dependencies

| Dependency | Version | Purpose |
|------------|---------|---------|
| Capacitor | 5.x+ | Web-to-Native bridge |
| Tailwind CSS | 3.x CDN | Styling framework |
| Gemini API | 2.5-flash | AI engine |

### Build Dependencies

| Dependency | Version | Purpose |
|------------|---------|---------|
| Gradle | 8.11+ | Build system |
| Android Gradle Plugin | 8.x | Android build |
| Java/Kotlin | 17+ | Compilation |

### No npm Dependencies!

Pure HTML/JS app - no package.json needed.

---

## Monitoring & Analytics

### Current Tracking

- **Console Logs**: Development debugging
- **Usage Toast**: Per-request token count
- **Error Notifications**: User-facing errors

### Future Analytics (Optional)

Could add:
- Firebase Analytics
- Error reporting (Sentry)
- Performance monitoring
- User behavior tracking

---

## API Costs Estimation

**Gemini 2.5 Flash Pricing** (as of 2025):
- Free tier: 1,500 requests/day
- Paid: ~$0.15 per 1M tokens

**Typical Usage:**
- Card lookup: ~2,000 tokens
- Recommendation: ~3,000 tokens
- 100 operations/month: ~300,000 tokens = ~$0.05

**Cost-effective for personal use!**

---

## Deployment Checklist

- [ ] Test on multiple devices
- [ ] Verify API key masking
- [ ] Check all animations
- [ ] Test error scenarios
- [ ] Validate localStorage persistence
- [ ] Review console for errors
- [ ] Test offline graceful degradation
- [ ] Verify S24 full-screen mode
- [ ] Check status bar icons (dark/light)
- [ ] Test rate limiting behavior
- [ ] Validate usage stats accuracy
- [ ] Check markdown rendering
- [ ] Test LaTeX cleanup
- [ ] Verify rupee symbol display

---

**Documentation Version:** 1.0  
**Last Updated:** 2025-11-12  
**Architecture Status:** ✅ Stable

