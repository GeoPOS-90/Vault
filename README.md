# Vault
================================================================================
DUNGEON VAULT NET WORTH CALCULATOR — MASTER SPECIFICATION DOCUMENT
Version: 4.4 Final
Last Updated: October 2026
================================================================================

PURPOSE
-------
This document contains all specifications, lessons learned, and build instructions
for the Dungeon Vault Net Worth Calculator. Use this to resume development in
a new session without losing context.

================================================================================
SECTION 1: CORE CONCEPT
================================================================================

A retro 16-bit dungeon/RPG themed personal net worth calculator with:
- Dual player profiles (King & Queen) with separate localStorage
- Combined Kingdom view showing both profiles merged
- Asset tracking across 5 categories
- Cash flow ledger with categorized expenses
- Historical snapshots and trend visualization
- Crystal ball future projections
- Privacy/stealth mode
- Export/Import JSON backup

================================================================================
SECTION 2: LESSONS LEARNED — MUST FOLLOW
================================================================================

#   | RULE
----|----------------------------------------------------------------------
1   | Font: ONLY "Press Start 2P" from Google Fonts — NEVER change
2   | Gold glow: color #ffd700 WITH REDUCED glow shadow:
    | text-shadow: 0 0 8px #ffd700, 0 0 15px #c9a227
    | NOT yellow with dark shadow
3   | Parchment inputs: background #d4c4a8, color #3d2914, 
    | border 2px solid #5c4033 — NO BLACK BACKGROUNDS on inputs
4   | Tab names: Use EXACT names specified — no changes unless told
5   | Dashboard + MAP = ONE tab (Treasury Hall) — no separate MAP tab
6   | Preserve ALL working features between versions
7   | Comma formatting ($1,234,567) on ALL input tabs and displays
8   | XAUS API primary for gold (xaus.com/api/v1/spot)
    | Gold-API fallback (api.gold-api.com/price/XAU)
9   | CoinGecko primary for BTC, XAUS fallback
10  | Stealth Mode toggle at TOP of Treasury Hall (prominent placement)
11  | Kingdom's Vault button next to Queen at top profile row
12  | Investment fields: 401(k), Roth IRA, Brokerage — NO themed renaming
13  | ALL input backgrounds must be parchment tan — verify every tab
14  | Kingdom's Vault = SIMPLE: Total Net Worth + Pie Chart only
15  | Expenses: Themed category HEADERS with Name + Amount rows under each
16  | Double-check EVERY input field styling before completing build
17  | Do NOT add themed names to investment fields unless explicitly told
18  | Category headers are static text, not dropdowns

================================================================================
SECTION 3: CONFIRMED TAB NAMES (LOCKED)
================================================================================

Tab             | Exact Name        | Emoji
----------------|-------------------|-------
Dashboard       | TREASURY HALL     | 🏠
Investments     | MARKET GUILD      | 🏦
Savings         | COIN VAULT        | 💰
Real Estate     | CASTLE            | 🏰
Gold            | GOLDEN TROVE      | 🪙
Bitcoin         | CRYPTO TOKENS     | ₿
Combined View   | KINGDOM'S VAULT   | 🏰

================================================================================
SECTION 4: INVESTMENT FIELD NAMES (LOCKED)
================================================================================

Field 1: 401(k)
Field 2: Roth IRA
Field 3: Brokerage

DO NOT rename these to themed names (Armory, Shield, Scrolls, etc.)

================================================================================
SECTION 5: EXPENSE CATEGORY HEADERS (LOCKED)
================================================================================

Category        | Themed Header Name
----------------|--------------------
Housing         | 🏰 KEEP & FORTRESS
Bills/Utilities | 🔥 TORCH & FLAME
Food/Groceries  | 🍖 PROVISIONS
Transportation  | 🐎 STABLE & STEED
Subscriptions   | 📜 GUILD DUES
Miscellaneous   | 🎲 BOUNTY & SPOILS

Structure: Each category is a HEADER (not dropdown), with dynamic rows beneath
for Name + Amount. Each category has its own ➕ ADD button.

================================================================================
SECTION 6: STYLING SPECIFICATIONS (LOCKED)
================================================================================

FONTS
-----
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
font-family: 'Press Start 2P', cursive;

COLORS
------
Gold text:        #ffd700
Gold glow shadow: text-shadow: 0 0 8px #ffd700, 0 0 15px #c9a227
Parchment bg:     #d4c4a8 or #e8dcc8
Parchment text:   #3d2914
Parchment border: #5c4033
Main background:  #1a1a2e
Stone containers: #2a2a3e
Stone border:     #4a4a5e
Torch glow:       box-shadow: 0 0 15px rgba(255, 150, 50, 0.3)

INPUT STYLING (ALL INPUTS)
--------------------------
input, select, textarea {
  background: #d4c4a8;
  color: #3d2914;
  border: 2px solid #5c4033;
  font-family: 'Press Start 2P', cursive;
  font-size: 10px;
  padding: 8px;
  border-radius: 4px;
}

input:focus, select:focus {
  outline: none;
  border-color: #ffd700;
  box-shadow: 0 0 8px rgba(255, 215, 0, 0.5);
}

HEADER TEXT STYLING
-------------------
h1, h2, .tab-header {
  color: #ffd700;
  text-shadow: 0 0 8px #ffd700, 0 0 15px #c9a227;
}

================================================================================
SECTION 7: PROFILE STRUCTURE
================================================================================

TOP ROW BUTTONS (left to right):
- 👑 KING'S VAULT
- 👸 QUEEN'S VAULT  
- 🏰 KINGDOM'S VAULT
- 📤 EXPORT
- 📥 IMPORT

Active profile has gold glowing border.
Kingdom's Vault is VIEW ONLY (reads both profiles, no editing).

================================================================================
SECTION 8: TAB SPECIFICATIONS
================================================================================

🏠 TREASURY HALL (Dashboard)
-----------------------------
- TOP: Stealth Mode toggle (🔒 STEALTH MODE / 👁 REVEAL TREASURES)
- Total Net Worth (large, gold glow)
- Category cards: Investments, Savings, Castle (equity), Gold, Bitcoin
  Each shows $ amount (with commas) and % of total
- Net Worth Goal: Target input + progress bar
- Pie Chart: Canvas, values+% on slices, crown in center (👑/👸)
- Legend: colors, names, values, percentages
- Historical: 📸 SAVE SNAPSHOT, line chart, history list, 🗑️ CLEAR HISTORY
- Collapsible Ledger: 📜 OPEN LEDGER button reveals cash flow section
  - Income: Monthly Take-Home Pay
  - Expenses: 6 category headers with dynamic rows
  - Summary: Total Expenses, Monthly Surplus, Savings Rate %

🏦 MARKET GUILD (Investments)
-----------------------------
- 401(k): Balance, Annual Contribution, Growth Rate %
- Roth IRA: Balance, Annual Contribution, Growth Rate %
- Brokerage: Balance, Annual Contribution, Growth Rate %
- All parchment styled inputs
- 🔮 CONSULT THE ORACLE (hidden by default)

💰 COIN VAULT (Savings)
-----------------------
- Cash/Emergency Fund: Balance, APY %
- Parchment inputs
- Crystal ball (hidden)

🏰 CASTLE (Real Estate)
-----------------------
- Property Market Value
- Outstanding Mortgage Balance
- Calculated Equity (auto-display)
- Mortgage Interest Rate %
- Payoff Target Year
- Appreciation Rate %
- Crystal ball (hidden)

🪙 GOLDEN TROVE (Gold)
----------------------
- Troy Ounces input
- ⚡ FETCH SPOT PRICE button
  Primary API: https://xaus.com/api/v1/spot
  Fallback: https://api.gold-api.com/price/XAU
- Manual Spot Price input ($/oz)
- Calculated Value display (oz × price)
- Last Updated timestamp
- Growth Rate %
- Crystal ball (hidden)

₿ CRYPTO TOKENS (Bitcoin)
-------------------------
- BTC Quantity input (decimals)
- ⚡ FETCH BTC PRICE button
  Primary API: https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd
  Fallback: XAUS API
- Manual Price input ($/BTC)
- Calculated Value display
- Last Updated timestamp
- Growth Rate %
- Crystal ball (hidden)

🏰 KINGDOM'S VAULT (Combined View)
----------------------------------
- Reads from BOTH king_vault_data AND queen_vault_data
- Shows ONLY:
  * Combined Total Net Worth (large, gold glow)
  * Combined Pie Chart (🏰 in center)
- NO breakdown tables
- NO individual King/Queen totals
- VIEW ONLY — no editing

================================================================================
SECTION 9: CRYSTAL BALL FEATURE
================================================================================

- Button text: "🔮 CONSULT THE ORACLE"
- Hidden by default on all asset tabs
- Click reveals:
  * Glowing orb animation (CSS pulsing glow)
  * Year slider (1 to 30 years)
  * Compound growth projection table
- Click again to collapse
- Uses growth rate % from that tab's inputs

================================================================================
SECTION 10: LOCALSTORAGE STRUCTURE
================================================================================

king_vault_data: {
  investments: {
    k401: {balance, contribution, growth},
    roth: {balance, contribution, growth},
    brokerage: {balance, contribution, growth}
  },
  savings: {balance, apy},
  realEstate: {value, mortgage, rate, payoffYear, appreciation},
  gold: {ounces, spotPrice, growth},
  bitcoin: {quantity, price, growth},
  expenses: {
    keepFortress: [{name, amount}, ...],
    torchFlame: [{name, amount}, ...],
    provisions: [{name, amount}, ...],
    stableSteed: [{name, amount}, ...],
    guildDues: [{name, amount}, ...],
    bountySpoils: [{name, amount}, ...]
  },
  income: number,
  goal: number
}

queen_vault_data: (same structure)

king_vault_history: [{date: "YYYY-MM-DD", netWorth: number}, ...]
queen_vault_history: [{date: "YYYY-MM-DD", netWorth: number}, ...]

================================================================================
SECTION 11: API ENDPOINTS
================================================================================

GOLD (Primary):
https://xaus.com/api/v1/spot
Response: {xau_usd_oz: number} or {spot_usd_oz: number}
Free, no API key, CORS enabled

GOLD (Fallback):
https://api.gold-api.com/price/XAU
Response: {price: number}
Free, no API key

BITCOIN (Primary):
https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd
Response: {bitcoin: {usd: number}}
Free, no API key

BITCOIN (Fallback):
Use XAUS API: {btc_usd: number}

================================================================================
SECTION 12: NUMBER FORMATTING
================================================================================

Helper function:
function formatCurrency(num) {
  return '$' + Number(num).toLocaleString('en-US', {
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  });
}

Apply to ALL displayed dollar amounts throughout the application.
Inputs accept raw numbers; displays show formatted with commas.

================================================================================
SECTION 13: FUTURE ENHANCEMENTS (DEFERRED)
================================================================================

- Additional historical trend chart options
- Multiple properties support
- Tax optimization calculator
- Retirement projection calculator
- Mobile app (PWA) with service worker
- Cloud sync option

================================================================================
SECTION 14: DEPLOYMENT OPTIONS
================================================================================

Option 1: Local HTML File
- Save as single .html file
- Open in any browser
- Data stored in browser localStorage

Option 2: GitHub Pages (Recommended for multi-device)
- Free hosting
- URL: https://yourusername.github.io/repo-name/
- Add PWA manifest for "Add to Home Screen" capability
- Data still stored locally per device

Option 3: PWA Package
- Add manifest.json
- Add service-worker.js
- Add app icons
- Enables offline capability and app-like experience

================================================================================
END OF DOCUMENT
================================================================================
