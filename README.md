# The Dumbest iPod Won

**Data Studio Project 2** | March 2026

An analysis of whether discontinued portable music players sell above their original retail price.

[View the published project](https://kylieklifton.github.io/ipod-analysis/)

---

## What I Set Out To Do

I wanted to test whether the "nostalgia economy" is real—do discontinued Apple devices actually appreciate in value, or is that just internet hype? Specifically, I analyzed iPods, the Zune HD, Sony Walkman, and Mac Mini M1 to see which (if any) are selling above their original MSRP.

---

## What I Found

**The iPod Shuffle is the clear winner.** It's the only device where even average listings sell above the original price (+33%). Premium-condition Shuffles go for 3x the original $49 price.

Five of nine devices showed appreciation in the premium tier:
- iPod Shuffle: +204%
- Mac Mini M1: +177%
- iPod Classic: +42%
- iPod Nano: +23%
- iPod Hi-Fi: +19%

The losers? Devices that tried to do too much. The iPod Touch (basically a worse iPhone) lost 66% of its value. The Zune HD, despite its cult following, is down 69%.

**The takeaway:** Simpler devices hold value. In an age of infinite distractions, a device that just plays music has found its moment.

---

## Data Collection

**Source:** eBay Browse API (current asking prices, not sold prices)

- 100 listings per device (900 total after excluding iPod 1st Gen as a collector outlier)
- No condition filter (includes all conditions from "For Parts" to "New/Sealed")
- Pulled on March 1, 2026

**The API Journey (Honest Reflection):**

I originally wanted sold price data from eBay's Finding API—what people actually paid, not just asking prices. After hours setting up API access (developer account, OAuth, Vercel verification endpoint), the Finding API rate-limited almost immediately. I never got to save that data.

**Lesson learned the hard way:** ALWAYS export data to CSV the moment an API works. Rate limits on new developer accounts are brutal.

I fell back to the Browse API, which only shows current listings. It's messier data (includes overpriced listings that will never sell), but it's what I had.

---

## Data Analysis

Analysis done in Python (Jupyter notebook) using pandas, numpy, and matplotlib.

Key metrics calculated:
- Median price vs. original MSRP
- Top 25% price tier (premium/mint condition listings)
- Percent change from MSRP for both tiers

The "Top 25%" metric turned out to be crucial—it reveals the premium that mint-condition devices command, which is where the real appreciation story lives.

---

## Files in This Repo

| File | Description |
|------|-------------|
| `ipod_price_analysis.ipynb` | Main analysis notebook |
| `ebay_browse_api_data.csv` | Summary statistics by device |
| `ebay_all_listings.csv` | All 900 individual listings |
| `mrsp_baseline_csv - Sheet1.csv` | Original MSRP data |
| `data_diary.md` | Process documentation |
| `index.html` | Article draft |

---

## What I Learned

- **API rate limits are real.** Test with small queries first. Save data immediately.
- **Condition filtering can hide your story.** I initially filtered to "Used - Good or better" and lost all the premium listings that showed appreciation.
- **The median isn't always the story.** Looking at price tiers (top 25%) revealed patterns the median obscured.

---

## What I'd Do With More Time

- Get actual sold price data (wait for Finding API rate limit to reset)
- Add more devices (colorful iMacs? original Game Boys?)
- Track prices over time to see if appreciation is accelerating
- Interview collectors directly, not just resellers

---

## Human Source

Mohammad Uddin, Manager of TSS Phones and Computers (New York)
10 years in the used device business
Interviewed in person, March 1, 2026

---

## AI Disclosure

Claude was used to assist with API integration and some data analysis to troubleshoot the API challenges.
