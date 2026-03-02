# The Dumbest iPod Won

**Data Studio Project 2** | March 2026

Looking at whether discontinued music players actually sell for more than they originally cost.

[View the published project](https://kylieklifton.github.io/ipod-analysis/)

---

## What I Was Trying To Do

I wanted to see if the "nostalgia economy" thing is real - do old Apple devices actually go up in value or is that just internet hype? I looked at iPods, the Zune HD, Sony Walkman, and Mac Mini M1 to see which ones are selling above their original price.

---

## What I Found

The iPod Shuffle is the winner. It's the only device where even average listings sell above the original price (+33%). Good condition Shuffles go for around 3x the original $49.

Five of nine devices showed gains in the premium tier:
- iPod Shuffle: +204%
- Mac Mini M1: +177%
- iPod Classic: +42%
- iPod Nano: +23%
- iPod Hi-Fi: +19%

The losers were devices that tried to do too much. iPod Touch lost 66% of its value - it's basically just a worse iPhone. Zune HD is down 69% even with its cult following.

Basically: simpler devices hold value better.

---

## Data Collection

**Source:** eBay Browse API (current asking prices, not sold prices)

- 100 listings per device (900 total after dropping iPod 1st Gen - it's a collector outlier)
- No condition filter - includes everything from "For Parts" to "New/Sealed"
- Pulled March 1, 2026

**What happened with the API:**

I originally wanted sold price data from eBay's Finding API - what people actually paid. After spending hours setting up API access (developer account, OAuth, Vercel endpoint), the Finding API rate-limited almost immediately. Never got to save that data.

Lesson: ALWAYS export to CSV the second an API works. Rate limits on new accounts are rough.

Had to fall back to the Browse API which only shows current listings. Messier data but it's what I had.

---

## Analysis

Used Python (Jupyter notebook) with pandas, numpy, and matplotlib.

What I calculated:
- Median price vs original MSRP
- Top 25% price tier (premium/mint listings)
- Percent change from MSRP for both

The top 25% metric ended up being important - that's where the appreciation story actually shows up.

---

## Files

| File | What it is |
|------|------------|
| `ipod_price_analysis.ipynb` | Main analysis notebook |
| `ebay_browse_api_data.csv` | Summary stats by device |
| `ebay_all_listings.csv` | All 900 listings |
| `mrsp_baseline_csv - Sheet1.csv` | Original MSRP data |
| `data_diary.md` | Process notes |
| `index.html` | Article |

---

## What I Learned

- API rate limits are real. Test with small queries first. Save data immediately.
- Condition filtering can hide your story. I filtered to "Used - Good or better" at first and lost all the premium listings.
- Median isn't always the story. Looking at the top 25% showed patterns the median hid.

---

## What I'd Do With More Time

- Get actual sold price data when the rate limit resets
- Add more devices (colorful iMacs? Game Boys?)
- Track prices over time
- Talk to collectors, not just resellers

---

## Source

Mohammad Uddin, Manager of TSS Phones and Computers (New York)
10 years in the used device business
Interviewed in person, March 1, 2026

---

## AI Disclosure

Used Claude for API integration, data analysis, and drafting. Conversation linked in submission.
