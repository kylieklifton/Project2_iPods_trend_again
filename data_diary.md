# Data Diary - iPod Price Analysis Project

## 2026-03-01

### Project Goal
Analyze whether discontinued portable music players sell above their original retail price.

---

### The API Journey (Honest Reflection)

**What I wanted:** Access to eBay's sold/completed listings data through the Finding API. This would show actual transaction prices—what people really paid—not just what sellers are asking.

**What happened:** I spent hours setting up eBay API access:
- Created a developer account
- Built a verification endpoint on Vercel
- Configured OAuth credentials
- Finally got production access

Then the Finding API ran out of tokens almost immediately.

**My biggest regret:** I didn't save the data to CSV before the rate limit hit. The API worked once—I saw real sold prices—and then it was gone. I can't get that data back until the rate limit resets (could be hours or days). For a project due today, that's devastating.

**What I learned the hard way:**
1. ALWAYS export data to CSV immediately when an API works
2. Rate limits on new developer accounts are brutal
3. The Finding API (sold items) has stricter limits than Browse API (current listings)

**What I had to do instead:** Fall back to the Browse API, which only shows current asking prices. This includes damaged items, parts, and overpriced listings that will never sell—it's messier data.

---

### Data Source (What I Actually Have)
- **Source:** eBay Browse API (current listings, NOT sold prices)
- **Listings per device:** 100 (equal sample sizes for fair comparison)
- **Total listings:** 1,000 across 10 devices
- **Condition filter:** None (all conditions included)
- **Date pulled:** March 1, 2026
- **Limitation:** These are asking prices, not verified sales

**Why no condition filter:** Including all conditions reveals the full price spectrum—from "for parts" junk to sealed collector pieces. This shows the real story: the *median* device depreciates, but *premium* condition devices can appreciate significantly.

---

### Devices Analyzed

| Device | Original MSRP | Listings | Condition |
|--------|---------------|----------|-----------|
| iPod Classic | $249 | 100 | Used - Good+ |
| iPod Mini | $249 | 100 | Used - Good+ |
| iPod Nano | $149 | 100 | Used - Good+ |
| iPod Shuffle | $49 | 100 | Used - Good+ |
| iPod Touch | $399 | 100 | Used - Good+ |
| iPod 1st Gen | $399 | 100 | Used - Good+ |
| iPod Hi-Fi | $349 | 100 | Used - Good+ |
| Zune HD | $290 | 100 | Used - Good+ |
| Sony Walkman | $298 | 100 | Used - Good+ |
| Mac Mini M1 | $699 | 100 | Used - Good+ |

---

### Key Findings

**The problem with median prices:** When you look at ALL listings, most devices appear to depreciate because the data includes damaged units, parts, and junk.

**The real story is in the premium tier.** When filtering for better-condition listings (top 25%), a different picture emerges:

| Device | MSRP | Top 25% Price | Change |
|--------|------|---------------|--------|
| iPod Shuffle | $49 | $130 | **+165%** |
| iPod Nano 7th Gen | $149 | $167 | **+12%** |
| iPod Hi-Fi | $349 | $390 | **+12%** |
| iPod Classic | $249 | $255 | **+2%** |
| iPod Touch | $399 | $260 | -35% |
| iPod Mini | $249 | $100 | -60% |

**The takeaway:** Condition is everything. Premium-condition discontinued devices CAN appreciate—but the average listing is junk.

---

### Files Created
- `ebay_browse_api_data.csv` — Summary statistics by device
- `ebay_all_listings.csv` — All 1,346 individual listings
- `ipod_price_analysis.ipynb` — Analysis notebook with charts

---

### Interview Questions for Used Tech Store
1. Do you see iPod Shuffles selling above their original $49 price?
2. How much does condition affect pricing for iPod Classics?
3. Have you ever had an iPod Hi-Fi come through? What did it sell for?
4. What's the most valuable iPod you've sold?

---

### Condition Filter Decision

**The confusion:** After adding a "Used - Good or better" condition filter, all devices showed depreciation below MSRP. The numbers looked much worse than before.

**What I realized:** The condition filter excluded New/Sealed listings—those rare, pristine units that command premium prices. By filtering them out, I removed the very data points that showed appreciation.

**The fix:** Removed the condition filter entirely. Now the data includes all conditions, which reveals the full price spectrum. The story becomes clearer: *condition is everything*. The median price (mostly used/worn units) depreciates, but the top 25% (mint/sealed) can appreciate significantly.

---

### What I Would Do Differently
- Save API data to CSV IMMEDIATELY
- Test rate limits with small queries first
- Have a backup data source ready
- Start earlier so rate limit resets aren't deadline-breaking
- Be careful with filters—they can accidentally remove the most interesting data
