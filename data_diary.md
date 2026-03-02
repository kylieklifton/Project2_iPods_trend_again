# Data Diary - iPod Price Analysis Project

### Project Goal
Figure out if discontinued music players are actually selling for more than they originally cost.

---

### The API Situation

**What I wanted:** Sold listing data from eBay's Finding API - actual prices people paid, not just what sellers are asking.

**What happened:** Spent way too long setting up eBay API access:
- Made a developer account
- Set up a verification endpoint on Vercel
- Got OAuth working
- Finally got production access

Then the Finding API hit its rate limit almost immediately.

**Biggest regret:** I didn't save the data to CSV before the rate limit kicked in. The API worked once and then it was gone. Can't get that data back until the limit resets. Not great when the project is due today.

**What I learned:**
1. ALWAYS save data to CSV right away when an API works
2. Rate limits on new accounts are rough
3. Finding API has stricter limits than Browse API

**What I ended up using:** The Browse API, which only shows current asking prices. It's messier - includes damaged items and overpriced stuff that'll never sell.

---

### Data Source
- **Source:** eBay Browse API (current listings, NOT sold prices)
- **Listings per device:** 100 each
- **Total:** 1,000 listings across 10 devices
- **Condition filter:** None - included everything
- **Date:** March 1, 2026
- **Limitation:** These are asking prices, not actual sales

Decided not to filter by condition because it shows the full range - from junky "for parts" listings to sealed collector pieces.

---

### Devices Analyzed

| Device | Original MSRP | Listings |
|--------|---------------|----------|
| iPod Classic | $249 | 100 |
| iPod Mini | $249 | 100 |
| iPod Nano | $149 | 100 |
| iPod Shuffle | $49 | 100 |
| iPod Touch | $399 | 100 |
| iPod 1st Gen | $399 | 100 |
| iPod Hi-Fi | $349 | 100 |
| Zune HD | $290 | 100 |
| Sony Walkman | $298 | 100 |
| Mac Mini M1 | $699 | 100 |

---

### Key Findings

Looking at median prices, most devices look like they depreciate. But that's because the data includes a lot of damaged units and junk.

The interesting stuff is in the top 25% tier (premium condition):

| Device | MSRP | Top 25% Price | Change |
|--------|------|---------------|--------|
| iPod Shuffle | $49 | $130 | +165% |
| iPod Nano | $149 | $167 | +12% |
| iPod Hi-Fi | $349 | $390 | +12% |
| iPod Classic | $249 | $255 | +2% |
| iPod Touch | $399 | $260 | -35% |
| iPod Mini | $249 | $100 | -60% |

Basically: condition matters a lot. Premium condition devices can appreciate, but the average listing is junk.

---

### Files
- `ebay_browse_api_data.csv` — Summary stats by device
- `ebay_all_listings.csv` — All the individual listings
- `ipod_price_analysis.ipynb` — Analysis notebook

---

### Interview Questions
1. Do you see iPod Shuffles selling above their original $49 price?
2. How much does condition affect pricing for iPod Classics?
3. Have you ever had an iPod Hi-Fi come through? What did it sell for?
4. What's the most valuable iPod you've sold?

---

### The Condition Filter Thing

At first I added a "Used - Good or better" filter and suddenly all the devices showed depreciation. The numbers looked way worse.

Then I realized the filter was excluding New/Sealed listings - the rare mint units that actually show appreciation. By filtering them out I was removing the interesting data.

So I took off the filter. Now the data shows the full picture: median prices depreciate, but top 25% can appreciate a lot.

---

### What I'd Do Differently
- Save API data to CSV right away
- Test rate limits with small queries first
- Have a backup data source ready
- Start earlier
- Be careful with filters - they can hide the good stuff
