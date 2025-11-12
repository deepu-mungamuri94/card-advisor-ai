# 🏗️ Architecture Documentation - Card Advisor AI

This document provides a comprehensive technical overview of Card Advisor AI's architecture, design decisions, and implementation details.

---

## 📑 Table of Contents

1. [High-Level Architecture](#high-level-architecture)
2. [Technology Stack](#technology-stack)
3. [Project Structure](#project-structure)
4. [Core Components](#core-components)
5. [Data Flow](#data-flow)
6. [AI Integration](#ai-integration)
7. [Storage Architecture](#storage-architecture)
8. [UI/UX Architecture](#uiux-architecture)
9. [Security Model](#security-model)
10. [Performance Optimizations](#performance-optimizations)
11. [Design Decisions](#design-decisions)
12. [API Reference](#api-reference)

---

## 🎯 High-Level Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Mobile Device (Android)                  │
│  ┌────────────────────────────────────────────────────────┐ │
│  │               Capacitor WebView Container              │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │         Web Application (HTML/JS/CSS)            │  │ │
│  │  │                                                   │  │ │
│  │  │  ┌────────────┐  ┌─────────────┐  ┌───────────┐ │  │ │
│  │  │  │ UI Layer   │  │ Logic Layer │  │  Storage  │ │  │ │
│  │  │  │            │  │             │  │   Layer   │ │  │ │
│  │  │  │ - Tailwind │  │ - Card Mgmt │  │           │ │  │ │
│  │  │  │ - HTML5    │  │ - AI Client │  │ localStorage│ │  │ │
│  │  │  │ - Markdown │  │ - Utils     │  │           │ │  │ │
│  │  │  └────────────┘  └─────────────┘  └───────────┘ │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────┘ │
│                            ↕                                 │
│            ┌───────────────────────────────┐                │
│            │   Capacitor Bridge (Native)   │                │
│            │   - WebView APIs              │                │
│            │   - Platform Integration      │                │
│            └───────────────────────────────┘                │
└─────────────────────────────────────────────────────────────┘
                            ↕ HTTPS
┌─────────────────────────────────────────────────────────────┐
│              Google Gemini API (Cloud)                       │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  Gemini 2.5 Flash Model + Google Search Tool          │ │
│  │  - Natural Language Processing                        │ │
│  │  - Real-Time Web Search                               │ │
│  │  - Structured Response Generation                     │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────────┐
│           Official Bank Websites (Searched by AI)           │
│  - HDFC Bank    - SBI Card    - ICICI Bank                  │
│  - Axis Bank    - AMEX        - Standard Chartered          │
└─────────────────────────────────────────────────────────────┘
```

### Architecture Type

**Hybrid Mobile Application**:
- **Frontend**: Web technologies (HTML5, JavaScript, CSS)
- **Runtime**: Native Android WebView via Capacitor
- **Backend**: Serverless (Gemini API as backend)
- **Storage**: Client-side only (localStorage)

**Key Characteristics**:
- **Single-page application** (SPA) pattern
- **Client-side rendering** (CSR)
- **Zero backend infrastructure**
- **API-first architecture**

---

## 🛠️ Technology Stack

### Frontend Layer

| Technology | Version | Purpose |
|------------|---------|---------|
| **HTML5** | Latest | Structure & semantics |
| **JavaScript** | ES6+ | Application logic |
| **Tailwind CSS** | 3.x (CDN) | Styling & responsive design |
| **Markdown** | Custom parser | Content formatting |

### Mobile Runtime

| Technology | Version | Purpose |
|------------|---------|---------|
| **Capacitor** | 6.x | Web-to-native bridge |
| **Android WebView** | System | JavaScript runtime |
| **Gradle** | 8.x | Build automation |

### AI & APIs

| Service | Model/Version | Purpose |
|---------|---------------|---------|
| **Google Gemini** | 2.5 Flash Preview | AI inference |
| **Google Search** | Integrated tool | Real-time web data |
| **REST API** | HTTPS | Communication protocol |

### Development Tools

| Tool | Purpose |
|------|---------|
| **Android Studio** | IDE, building, debugging |
| **Chrome DevTools** | WebView debugging |
| **Git** | Version control |
| **Node.js** | Capacitor CLI |

---

## 📂 Project Structure

### Directory Layout

```
cardadvisorapp/
│
├── android/                          # Native Android project (auto-generated)
│   ├── app/
│   │   ├── src/main/
│   │   │   ├── assets/
│   │   │   │   └── public/           # Web assets (copied from www/)
│   │   │   │       ├── index.html    # Main app file
│   │   │   │       └── capacitor.config.json
│   │   │   ├── java/com/mycompany/cardadvisor/
│   │   │   │   └── MainActivity.java # Capacitor bridge activity
│   │   │   └── res/                  # Android resources
│   │   │       ├── drawable/         # Icons
│   │   │       ├── mipmap-*/         # Launcher icons
│   │   │       ├── values/           # Strings, colors, styles
│   │   │       └── xml/              # Android configs
│   │   ├── build.gradle              # App-level Gradle config
│   │   └── proguard-rules.pro        # Code obfuscation rules
│   ├── gradle/                       # Gradle wrapper
│   ├── build.gradle                  # Project-level Gradle config
│   ├── settings.gradle               # Gradle settings
│   └── local.properties              # Local SDK path
│
├── www/                              # Web application source
│   ├── index.html                    # Complete app (~1650 lines)
│   │                                 # Contains:
│   │                                 # - HTML structure
│   │                                 # - Inline CSS styles
│   │                                 # - Inline JavaScript logic
│   │                                 # - All components & functions
│   └── (no other files)              # Single-file architecture
│
├── node_modules/                     # Node dependencies (if any)
│
├── capacitor.config.json             # Capacitor configuration
├── package.json                      # Node package manifest
├── package-lock.json                 # Locked dependencies
│
├── README.md                         # Main documentation
├── QUICKSTART.md                     # Setup guide
├── ARCHITECTURE.md                   # This file
│
├── icon-design.svg                   # App icon source
├── .gitignore                        # Git ignore rules
└── local.properties                  # Android SDK path
```

### Single-File Architecture

**Why one HTML file?**

1. **Simplicity**: No module bundler needed
2. **WebView Compatibility**: Avoids ES6 module issues
3. **Inline Everything**: CSS and JS embedded
4. **Zero Build Step**: Edit and copy - that's it
5. **Easy Debugging**: All code in one place

**www/index.html Structure** (~1650 lines):

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Meta tags, Tailwind CDN -->
    <style>
      /* Inline CSS (~100 lines) */
      /* - Custom animations */
      /* - Safe area handling */
      /* - Markdown styling */
    </style>
  </head>
  <body>
    <!-- Modals (~300 lines) -->
    <!-- - View Rules Modal -->
    <!-- - Rename Card Modal -->
    <!-- - Settings Modal -->
    
    <!-- Side Menu (~80 lines) -->
    <!-- Navigation drawer -->
    
    <!-- Header (~50 lines) -->
    <!-- App branding, menu button -->
    
    <!-- Main Content (~200 lines) -->
    <!-- - AI Advisor View -->
    <!-- - My Cards View -->
    
    <!-- Notification Toast (~20 lines) -->
    
    <script>
      /* Application Logic (~900 lines) */
      
      /* === Storage Layer === */
      /* - getApiKey() */
      /* - saveApiKey() */
      /* - loadCardsFromStorage() */
      /* - saveCardsToStorage() */
      
      /* === UI Functions === */
      /* - openMenu(), closeMenu() */
      /* - navigateTo(view) */
      /* - openModal(), closeModal() */
      /* - showNotification() */
      /* - displayUsageStats() */
      
      /* === Card Management === */
      /* - renderCards() */
      /* - addNewCard() */
      /* - deleteCard() */
      /* - updateCardName() */
      /* - openViewRulesModal() */
      /* - reloadRulesInModal() */
      
      /* === AI Integration === */
      /* - fetchGeminiResponse() */
      /* - fetchAndSaveCardRules() */
      /* - refreshCardRules() */
      /* - generateSuggestion() */
      
      /* === Utilities === */
      /* - markdownToHtml() */
      /* - updateCardCount() */
      /* - isApiKeyConfigured() */
      
      /* === Event Listeners === */
      /* - DOMContentLoaded */
    </script>
  </body>
</html>
```

---

## 🔧 Core Components

### 1. Storage Layer

**Technology**: localStorage (Browser API)

**Key-Value Store**:
```javascript
// API Key Storage
localStorage.setItem('geminiApiKey', 'AIza...');
let apiKey = localStorage.getItem('geminiApiKey');

// Cards Storage
localStorage.setItem('cardAdvisorCards', JSON.stringify(cards));
let cards = JSON.parse(localStorage.getItem('cardAdvisorCards') || '[]');
```

**Data Structure**:
```javascript
// Card Object
{
  id: "hdfc_millennia_credit_card",    // Unique identifier
  name: "HDFC Millennia Credit Card",  // Display name
  rules: "### Base Rewards\n- 1%..."   // Markdown formatted rules
}

// Cards Array
[
  { id: "card1", name: "...", rules: "..." },
  { id: "card2", name: "...", rules: "..." },
  ...
]
```

**Storage Functions**:
```javascript
function loadCardsFromStorage() {
  const stored = localStorage.getItem('cardAdvisorCards');
  return stored ? JSON.parse(stored) : [];
}

function saveCardsToStorage(cards) {
  localStorage.setItem('cardAdvisorCards', JSON.stringify(cards));
}
```

---

### 2. AI Integration Layer

**Provider**: Google Gemini API

**Endpoint**:
```
https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent
```

**Request Structure**:
```javascript
{
  "contents": [
    {
      "parts": [
        { "text": "User query here" }
      ]
    }
  ],
  "tools": [
    { "google_search": {} }  // Enable web search
  ],
  "systemInstruction": {
    "parts": [
      { "text": "System prompt with instructions" }
    ]
  }
}
```

**Response Structure**:
```javascript
{
  "candidates": [
    {
      "content": {
        "parts": [
          { "text": "AI response here" }
        ]
      }
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 1200,
    "candidatesTokenCount": 1250,
    "totalTokenCount": 2450
  }
}
```

**Core AI Function**:
```javascript
async function fetchGeminiResponse(systemPrompt, userQuery) {
  const apiKey = getApiKey();
  const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
  
  const payload = {
    contents: [{ parts: [{ text: userQuery }] }],
    tools: [{ "google_search": {} }],
    systemInstruction: { parts: [{ text: systemPrompt }] }
  };
  
  const response = await fetch(apiUrl, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  });
  
  const result = await response.json();
  return {
    text: result.candidates[0].content.parts[0].text,
    usage: result.usageMetadata
  };
}
```

---

### 3. UI Component Layer

**Framework**: Vanilla JavaScript + Tailwind CSS

**View Management**:
```javascript
const views = {
  advisor: document.getElementById('advisor-tab-content'),
  cards: document.getElementById('cards-tab-content')
};

function navigateTo(view) {
  // Hide all views
  Object.values(views).forEach(v => v.classList.add('hidden'));
  
  // Show selected view
  views[view].classList.remove('hidden');
  
  // Close menu
  closeMenu();
}
```

**Modal System**:
```javascript
// View Rules Modal
function openViewRulesModal(cardId, cardName) {
  // Find card
  const card = cardList.find(c => c.id === cardId);
  
  // Populate modal
  document.getElementById('view-rules-card-name').textContent = cardName;
  document.getElementById('view-rules-content').innerHTML = markdownToHtml(card.rules);
  
  // Show modal
  document.getElementById('view-rules-modal').classList.remove('hidden');
  
  // Store for reload
  currentViewingCardId = cardId;
}

function closeViewRulesModal() {
  document.getElementById('view-rules-modal').classList.add('hidden');
  currentViewingCardId = null;
}
```

**Notification System**:
```javascript
function showNotification(message, isError) {
  const notification = document.getElementById('notification');
  notification.textContent = message;
  notification.className = isError ? 'error-class' : 'success-class';
  notification.classList.remove('hidden');
  
  setTimeout(() => {
    notification.classList.add('hidden');
  }, 3000);
}
```

---

### 4. Markdown Rendering Engine

**Purpose**: Convert AI's markdown responses to styled HTML

**Supported Features**:
- Headings (`#`, `##`, `###`)
- Bold (`**text**`, `__text__`)
- Italic (`*text*`, `_text_`)
- Inline code (`` `code` ``)
- Code blocks (``` ``` ```)
- Lists (ordered and unordered)
- Paragraphs
- Line breaks

**Implementation**:
```javascript
function markdownToHtml(markdown) {
  let html = markdown;
  
  // LaTeX cleanup
  html = html.replace(/\$\\times\$/g, '×');
  html = html.replace(/\\text\{([^}]+)\}/g, '$1');
  html = html.replace(/\$([0-9,]+)/g, '₹$1');
  
  // Headings
  html = html.replace(/^### (.+)$/gm, '<h3 class="text-lg font-bold text-indigo-800 mt-4 mb-2">$1</h3>');
  html = html.replace(/^## (.+)$/gm, '<h2 class="text-xl font-bold text-indigo-900 mt-5 mb-3">$1</h2>');
  html = html.replace(/^# (.+)$/gm, '<h1 class="text-2xl font-bold text-gray-900 mt-6 mb-4">$1</h1>');
  
  // Bold
  html = html.replace(/\*\*(.+?)\*\*/g, '<strong class="text-indigo-700">$1</strong>');
  html = html.replace(/__(.+?)__/g, '<strong class="text-indigo-700">$1</strong>');
  
  // Italic
  html = html.replace(/\*(.+?)\*/g, '<em class="italic text-gray-700">$1</em>');
  html = html.replace(/_(.+?)_/g, '<em class="italic text-gray-700">$1</em>');
  
  // Lists
  html = html.replace(/^- (.+)$/gm, '<li class="ml-4 text-gray-700">• $1</li>');
  html = html.replace(/^(\d+)\. (.+)$/gm, '<li class="ml-4 text-gray-700"><span class="text-indigo-600 font-semibold">$1.</span> $2</li>');
  
  // Wrap lists
  html = html.replace(/(<li class="ml-4[^>]*>.*<\/li>)+/gs, '<ul class="space-y-1 my-3">$&</ul>');
  
  // Highlight currency
  html = html.replace(/₹([0-9,]+)/g, '<span class="text-green-600 font-semibold">₹$1</span>');
  
  // Highlight percentages
  html = html.replace(/(\d+(?:\.\d+)?%)/g, '<span class="text-blue-600 font-semibold">$1</span>');
  
  return html;
}
```

---

## 🔄 Data Flow

### Card Addition Flow

```
User Input
    ↓
[Enter Card Name] → "HDFC Millennia Credit Card"
    ↓
[Click "Fetch & Save"]
    ↓
fetchAndSaveCardRules()
    ↓
Build AI Prompt
    ↓
    ├─ System Prompt (70+ categories template)
    └─ User Query ("Fetch complete rules for HDFC Millennia...")
    ↓
fetchGeminiResponse()
    ↓
HTTP POST → Google Gemini API
    ↓
Gemini searches official bank website
    ↓
Gemini extracts comprehensive rules
    ↓
Response received
    ↓
    ├─ text: Markdown formatted rules
    └─ usage: { promptTokens, responseTokens, totalTokens }
    ↓
Create Card Object
    ↓
    {
      id: "hdfc_millennia_credit_card",
      name: "HDFC Millennia Credit Card",
      rules: "### Base Rewards\n- 1%..."
    }
    ↓
Add to cardList array
    ↓
saveCardsToStorage() → localStorage.setItem()
    ↓
renderCards() → Update UI
    ↓
displayUsageStats() → Show toast
    ↓
Done ✓
```

---

### Recommendation Flow

```
User Input
    ↓
[Enter Query] → "Buying ₹5,000 groceries at BigBasket"
    ↓
[Click "Get Best Card Suggestion"]
    ↓
generateSuggestion()
    ↓
Load all cards from cardList
    ↓
Build AI Prompt
    ↓
    ├─ System Prompt (recommendation instructions)
    └─ User Query + All Card Rules
    ↓
fetchGeminiResponse()
    ↓
HTTP POST → Google Gemini API
    ↓
Gemini analyzes:
    ├─ Purchase category
    ├─ Amount (₹5,000)
    ├─ Merchant (BigBasket)
    └─ All card reward rates
    ↓
Gemini calculates:
    ├─ Card A: 5% = ₹250
    ├─ Card B: 2% = ₹100
    └─ Card C: 1% = ₹50
    ↓
Response received
    ↓
    {
      text: "✅ Use HDFC Millennia\n💰 Earn ₹250...",
      usage: { ... }
    }
    ↓
markdownToHtml() → Convert to styled HTML
    ↓
Display in suggestion-result div
    ↓
displayUsageStats() → Show toast
    ↓
Done ✓
```

---

### Modal View & Reload Flow

```
User Action
    ↓
[Click 👁️ Eye Icon] on card
    ↓
openViewRulesModal(cardId, cardName)
    ↓
Find card in cardList
    ↓
Render rules: markdownToHtml(card.rules)
    ↓
Show modal (classList.remove('hidden'))
    ↓
Store currentViewingCardId (for reload)
    ↓
Modal Displayed ✓
    ↓
    ↓ [User clicks "Reload Rules"]
    ↓
reloadRulesInModal()
    ↓
Show loading animation
    ↓
Call refreshCardRules(currentViewingCardId, cardName)
    ↓
Fetch fresh rules from bank website
    ↓
Update cardList[cardId].rules
    ↓
Save to localStorage
    ↓
Update card list view (renderCards)
    ↓
Update modal content (markdownToHtml)
    ↓
Hide loading, restore button
    ↓
Done ✓
```

---

## 🧠 AI Integration

### Prompt Engineering

**System Prompt Structure** (~600 lines):

```javascript
const systemPrompt = `You are a financial information specialist with access to real-time web search via Google Search. Your task is to:

1. Search the OFFICIAL BANK WEBSITE for the "${cardName}" credit card (e.g., HDFC Bank, SBI Card, ICICI, Axis Bank official sites).

2. Verify information from the bank's official reward program terms and conditions.

3. Provide a COMPREHENSIVE, COMPLETE, MOBILE-FRIENDLY summary using BULLET POINTS (no tables!) of ALL verified benefits:

**MUST INCLUDE ALL OF THE FOLLOWING CATEGORIES (if available):**

**BASE REWARDS:**
- Base Reward Point (RP) earning rate per ₹100 or ₹150 spent (or Cashback %)
- Milestone benefits and annual spend bonuses

**HEALTHCARE & MEDICAL:**
- Pharmacy purchases (MedPlus, Apollo Pharmacy, Netmeds, 1mg)
- Hospital and clinic payments
- Health insurance premium payments
- Medical equipment and supplies
- Diagnostic tests and health checkups

[... 13 more major categories with 70+ subcategories ...]

4. COMPLETENESS RULES (CRITICAL):
- DO NOT TRUNCATE or summarize - include ALL offers found on the official website
- Check EVERY category listed above - don't skip categories
- If there are 20 benefits, list all 20 - don't leave anything out
- Be especially thorough with:
  * Movie ticket offers (BookMyShow 1+1) - present in most premium cards
  * Grocery rewards - often have special accelerated rates
  * Fuel surcharge waivers - common benefit
  * Healthcare/Pharmacy - increasingly popular benefit
- Include monthly/quarterly/annual caps for each category
- Mention if a category is EXCLUDED (0 rewards) - this is important info too

5. FORMATTING RULES:
- Use simple bullet points (- or *), NOT tables or complex formatting
- Use bold (**text**) for emphasis on offer names
- Keep lines short for mobile readability
- Use clear section headings (### Heading)
- ABSOLUTELY NO LaTeX: no $...$ math mode, no \\text{}, no \\times, no \\$
- For multiplication use "×" or "x", NOT \\times or $\\times$
- Write as plain text/Markdown only

6. CURRENCY RULES (CRITICAL):
- ALL amounts must be in Indian Rupees (₹) ONLY
- Never use $ or dollars - this is for INDIAN credit cards
- Example: ₹100, ₹1,000, ₹50 cashback

7. SOURCE VERIFICATION:
- Use ONLY official bank sources as the source of truth
- If specific benefit not found on official site, don't make it up
- But be thorough - check rewards page, terms & conditions, feature highlights`;
```

**User Query Structure**:

```javascript
const userQuery = `Search the official "${cardName}" bank website and fetch COMPLETE, COMPREHENSIVE reward rules for ALL spending categories:

MUST COVER (if available):
- Healthcare/Medical/Pharmacy
- Groceries/Supermarkets
- Fuel/Petrol stations
- Dining/Restaurants/Food delivery
- Entertainment (Movie tickets - BookMyShow 1+1 offers, OTT subscriptions)
- Travel (Flights, Hotels, Lounge access, Cabs)
- Online Shopping (Amazon, Flipkart, etc.)
- Offline Shopping (Malls, Electronics, Fashion)
- Utilities (Bills, Recharge)
- Insurance premiums
- Education fees
- Lifestyle/Wellness

DO NOT TRUNCATE or skip any category - list ALL offers, cashback rates, and reward points for EVERY category found on official website. Use bullet points, NO TABLES. Format in RUPEES (₹) for INDIAN market.`;
```

### API Configuration

**Model Selection**:
- **Model**: `gemini-2.5-flash-preview-09-2025`
- **Why Flash**: Fast response, good quality, cost-effective
- **Why 2.5**: Latest model with improved reasoning

**Tools Integration**:
```javascript
"tools": [{ "google_search": {} }]
```
- Enables real-time web search
- AI searches official bank websites
- Verifies from T&C pages
- Always up-to-date information

**Rate Limiting**:
```javascript
// Retry with exponential backoff
const delays = [2000, 4000, 8000]; // 2s, 4s, 8s
for (let attempt = 0; attempt < maxRetries; attempt++) {
  try {
    const response = await fetch(apiUrl, payload);
    if (response.status === 429) {
      await sleep(delays[attempt]);
      continue;
    }
    return response;
  } catch (error) {
    if (attempt === maxRetries - 1) throw error;
  }
}
```

---

## 🎨 UI/UX Architecture

### Responsive Design

**Viewport Configuration**:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
```

**Safe Area Handling**:
```css
body {
  padding-top: env(safe-area-inset-top);
  padding-bottom: env(safe-area-inset-bottom);
}

header {
  padding-top: calc(env(safe-area-inset-top) + 1rem);
  margin-top: 0.5rem;
}

#side-menu .header {
  padding-top: calc(env(safe-area-inset-top) + 1.5rem);
}
```

**Benefits**:
- Content never hidden behind notch/camera
- Proper spacing on all devices
- Works with different screen shapes

### Component Hierarchy

```
App Root
│
├── Modals (z-index: 50+)
│   ├── View Rules Modal
│   │   ├── Gradient Header
│   │   ├── Scrollable Content
│   │   └── Action Footer
│   ├── Rename Card Modal
│   └── Settings Modal
│
├── Side Menu (z-index: 50)
│   ├── Branded Header
│   └── Navigation Links
│
├── Header (sticky top)
│   ├── Menu Button
│   ├── App Icon
│   ├── App Name
│   └── Card Count Badge
│
├── Main Content
│   ├── AI Advisor View
│   │   ├── Query Input
│   │   ├── Submit Button
│   │   └── Results Display
│   │
│   └── My Cards View
│       ├── Add Card Form
│       └── Card List
│           └── Card Item
│               ├── Card Icon
│               ├── Card Name
│               ├── Edit Button
│               └── Actions (View, Reload, Delete)
│
└── Toast Notification (z-index: 50)
    └── Usage Stats
```

### Animation System

**CSS Animations**:
```css
@keyframes gradientShift {
  0% { background-position: 0% 50%, 0% 0%; }
  50% { background-position: 100% 50%, 0% 0%; }
  100% { background-position: 0% 50%, 0% 0%; }
}

@keyframes blink-red {
  0%, 100% { background-color: transparent; }
  50% { background-color: rgba(239, 68, 68, 0.2); }
}

.animate-spin {
  animation: spin 1s linear infinite;
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
```

**JavaScript Animations**:
```javascript
// Smooth transitions
element.classList.add('transition-all', 'duration-200');

// Toast auto-dismiss
setTimeout(() => {
  toast.classList.add('opacity-0');
  setTimeout(() => toast.classList.add('hidden'), 300);
}, 3000);

// Delete blink
deleteBtn.classList.add('blink-delete');
setTimeout(() => deleteBtn.classList.remove('blink-delete'), 500);
```

---

## 🔒 Security Model

### Threat Model

**Assets to Protect**:
- User's Gemini API key
- Credit card portfolio data
- API usage information

**Threat Actors**:
- Malicious apps on device
- Man-in-the-middle attacks
- Unauthorized API usage

**Mitigations**:
- ✅ localStorage (sandboxed per-app)
- ✅ HTTPS-only API calls
- ✅ No backend to compromise
- ✅ No user accounts to hack

### Data Security

**localStorage Security**:
```javascript
// Sandboxed per WebView
// Other apps cannot access
// Survives app restarts
// Cleared on app uninstall
localStorage.setItem('geminiApiKey', apiKey);
```

**API Key Handling**:
```html
<!-- Always masked -->
<input type="password" id="api-key-input" />

<!-- Never logged -->
console.log(apiKey); // ❌ Never do this

<!-- Only sent to Gemini API -->
fetch(geminiUrl, { headers: { 'Authorization': `Bearer ${apiKey}` } });
```

**Network Security**:
- ✅ HTTPS enforced for all API calls
- ✅ Certificate pinning (Android WebView)
- ✅ No plaintext transmission
- ✅ TLS 1.2+ required

### Privacy

**Data Collection**:
- ❌ No analytics
- ❌ No crash reporting
- ❌ No user tracking
- ❌ No telemetry

**Data Sharing**:
- ❌ No cloud sync
- ❌ No third-party services (except Gemini API)
- ❌ No social integrations
- ❌ No advertising networks

**Permissions**:
```xml
<!-- AndroidManifest.xml -->
<uses-permission android:name="android.permission.INTERNET"/>
<!-- That's it! No other permissions -->
```

---

## ⚡ Performance Optimizations

### Frontend Optimizations

**1. Lazy Loading**:
```javascript
// Cards rendered on-demand
function renderCards() {
  container.innerHTML = ''; // Clear first
  cardList.forEach(card => {
    const cardEl = document.createElement('div');
    cardEl.innerHTML = cardHTML;
    container.appendChild(cardEl);
  });
}
```

**2. Debouncing**:
```javascript
// Prevent rapid API calls
let lastRequestTime = 0;
const MIN_REQUEST_INTERVAL = 2000;

if (Date.now() - lastRequestTime < MIN_REQUEST_INTERVAL) {
  showNotification('Please wait before making another request', true);
  return;
}
```

**3. Efficient DOM Updates**:
```javascript
// Update only changed elements
function updateCardCount() {
  const badge = document.getElementById('card-count-badge');
  const count = cardList.length;
  badge.textContent = count;
  badge.classList.toggle('hidden', count === 0);
}
```

### Network Optimizations

**1. Request Caching**:
```javascript
// Cache card rules locally
localStorage.setItem('cardAdvisorCards', JSON.stringify(cards));

// No need to re-fetch unless user triggers refresh
```

**2. Retry Strategy**:
```javascript
// Exponential backoff for failed requests
const delays = [1000, 2000, 4000, 8000];
```

**3. Minimal Payload**:
```javascript
// Only send necessary data
{
  contents: [{ parts: [{ text: query }] }],
  tools: [{ google_search: {} }],
  systemInstruction: { parts: [{ text: prompt }] }
}
```

### Storage Optimizations

**1. Efficient Serialization**:
```javascript
// Compact JSON storage
localStorage.setItem('cards', JSON.stringify(cards));

// No whitespace, minimal overhead
```

**2. Selective Updates**:
```javascript
// Update only changed cards
function updateCard(cardId, newRules) {
  const index = cardList.findIndex(c => c.id === cardId);
  cardList[index].rules = newRules;
  saveCardsToStorage(); // Only save changed data
}
```

---

## 🎯 Design Decisions

### Why Capacitor over Native?

**Pros**:
- ✅ Write once, run on Android (and iOS if needed)
- ✅ Web technologies (HTML/CSS/JS) - faster development
- ✅ No native code knowledge required
- ✅ Hot reload during development
- ✅ Easy debugging (Chrome DevTools)

**Cons**:
- ❌ Slightly larger APK size
- ❌ Dependency on WebView performance
- ❌ Limited access to cutting-edge native APIs

**Decision**: **Pros outweigh cons** for this use case.

---

### Why Single HTML File?

**Pros**:
- ✅ No build process required
- ✅ No module bundler (webpack, rollup)
- ✅ Zero configuration
- ✅ WebView compatible (no ES6 module issues)
- ✅ Easy to debug (all code in one place)
- ✅ Instant changes (edit, copy, rebuild)

**Cons**:
- ❌ Large file (~1650 lines)
- ❌ No code splitting
- ❌ No tree shaking
- ❌ Harder to navigate

**Decision**: **Simplicity wins** for solo developer project.

---

### Why localStorage over Firebase?

**Pros**:
- ✅ Zero backend setup
- ✅ No authentication required
- ✅ No network dependency (offline-first)
- ✅ Instant reads/writes
- ✅ Complete privacy (data never leaves device)
- ✅ No quota limits
- ✅ No billing surprises

**Cons**:
- ❌ No cross-device sync
- ❌ No cloud backup
- ❌ Lost on app uninstall
- ❌ Limited storage (~5-10 MB)

**Decision**: **Privacy and simplicity** more important than sync.

---

### Why Gemini over OpenAI?

**Pros**:
- ✅ Free tier (1,500 requests/day)
- ✅ Google Search integration (built-in tool)
- ✅ Latest 2.5 Flash model (fast + good quality)
- ✅ No credit card required
- ✅ Generous token limits
- ✅ Real-time web search capability

**Cons**:
- ❌ Less ecosystem than OpenAI
- ❌ Fewer third-party tools

**Decision**: **Free tier and search integration** are key.

---

### Why Inline CSS/JS?

**Pros**:
- ✅ No external file loading
- ✅ Single HTTP request (index.html only)
- ✅ No CORS issues
- ✅ Guaranteed to work in WebView
- ✅ No build step

**Cons**:
- ❌ Harder to maintain
- ❌ No syntax highlighting (IDE limitations)
- ❌ No CSS preprocessor
- ❌ No TypeScript

**Decision**: **Reliability over developer convenience**.

---

## 📚 API Reference

### Storage API

```javascript
// Get API key
function getApiKey() {
  return localStorage.getItem('geminiApiKey') || '';
}

// Save API key
function saveApiKeyToStorage(key) {
  localStorage.setItem('geminiApiKey', key);
}

// Load cards
function loadCardsFromStorage() {
  const stored = localStorage.getItem('cardAdvisorCards');
  return stored ? JSON.parse(stored) : [];
}

// Save cards
function saveCardsToStorage(cards) {
  localStorage.setItem('cardAdvisorCards', JSON.stringify(cards));
}
```

---

### UI API

```javascript
// Navigation
function navigateTo(view)         // 'advisor' | 'cards'
function openMenu()
function closeMenu()

// Modals
function openViewRulesModal(cardId, cardName)
function closeViewRulesModal()
function openRenameModal(cardId, currentName)
function closeRenameModal()
function openSettingsModal()
function closeSettingsModal()

// Notifications
function showNotification(message, isError)
function displayUsageStats(usage)
```

---

### Card Management API

```javascript
// Render
function renderCards()
function updateCardCount()

// CRUD Operations
function addNewCard()                                 // Create
function deleteCard(cardId, cardName)                 // Delete
function updateCardName()                             // Update

// AI Integration
function fetchAndSaveCardRules()                      // Fetch from AI
function refreshCardRules(cardId, cardName)          // Refresh from AI
function reloadRulesInModal()                         // Reload in modal
```

---

### AI API

```javascript
// Core AI function
async function fetchGeminiResponse(systemPrompt, userQuery)
// Returns: { text: string, usage: { promptTokens, responseTokens, totalTokens, requestCount } }

// High-level functions
async function generateSuggestion()                   // Get recommendation
async function fetchAndSaveCardRules()                // Fetch card rules
async function refreshCardRules(cardId, cardName)    // Refresh rules
```

---

### Utility API

```javascript
// Markdown
function markdownToHtml(markdown)                     // Convert MD to HTML

// Validation
function isApiKeyConfigured()                         // Check if key exists

// State
let cardList = []                                     // Global card array
let currentViewingCardId = null                       // Modal state
```

---

## 🔮 Future Architecture Considerations

### Scalability

**Current Limits**:
- localStorage: ~5-10 MB
- ~50-100 cards max (theoretical)
- Single user per device

**If scaling needed**:
- Use IndexedDB for larger storage
- Implement pagination for card list
- Add search/filter functionality

---

### Modularity

**Current**: Monolithic single file

**Future Option**: Modular architecture
```
www/
├── index.html (shell)
├── js/
│   ├── storage.js
│   ├── ai.js
│   ├── ui.js
│   ├── cards.js
│   └── utils.js
└── css/
    └── app.css
```

**Trade-off**: Complexity vs. maintainability

---

### Backend Integration

**Current**: Serverless (API-only)

**Future Option**: Optional backend
```
Benefits:
- Cross-device sync
- Cloud backup
- User accounts
- Analytics (privacy-respecting)

Challenges:
- Infrastructure cost
- Privacy concerns
- Complexity increase
```

---

## 📝 Summary

### Key Architectural Strengths

1. ✅ **Simple**: One HTML file, zero backend
2. ✅ **Fast**: Instant load, local storage
3. ✅ **Private**: No cloud, no tracking
4. ✅ **Reliable**: Offline-first, minimal dependencies
5. ✅ **Maintainable**: Clear structure, inline everything
6. ✅ **Secure**: Sandboxed storage, HTTPS API

### Trade-offs Accepted

1. ⚠️ Large single file (manageable for solo dev)
2. ⚠️ No cross-device sync (privacy trade-off)
3. ⚠️ WebView performance (acceptable for use case)
4. ⚠️ Manual build process (simple enough)

### Result

**A lean, privacy-focused, AI-powered credit card advisor that works beautifully on Android without any backend infrastructure.**

---

**Architecture Document Version**: 1.1  
**Last Updated**: January 2025  
**Maintained by**: Deepu Mungamuri

