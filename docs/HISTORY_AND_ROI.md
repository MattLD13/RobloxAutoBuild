# How Roblox 3D hits were built, and what ROI looks like

## Quick summary

| | Amount (estimate) |
|---|---|
| **Cost per game** | **≈ $500** (range $200–$1,000): AI usage $50–$300 + launch ads $100–$500 + a share of the Studio computer |
| **Most likely return** | **$0–$100.** Most games never earn enough to cash out (minimum 30,000 Robux ≈ $114) |
| **Decent game** | $500–$5,000 total |
| **Rare hit** | $20,000 to millions |
| **Average per game** | Unknown until about 10–20 games have shipped. Expect most games to lose money and one rare hit to pay for the rest |

**Budget setup (owner's current hardware: Ryzen 5900X, 32 GB RAM, RTX 5090, Claude Pro):** extra cost per game is **≈ $0–$20**.

| Item | Cost |
|---|---|
| Roblox Studio, publishing, and the Open Cloud APIs | Free |
| AI building | Covered by the Pro subscription (limited by usage limits, so slower) |
| Icons, thumbnails, and 3D models | Free: Roblox's built-in generators, or local models on the 5090 |
| Electricity | ≈ $1–$3 (estimate) |
| Launch ads | $0–$15 (optional small test) |

Compiled Oct 2026. Most numbers come from press coverage and community analysis, not audited financials. Each figure links to its source. Figures marked **estimate** are my own arithmetic or assumptions.

---

## 1. How the big games were actually made

| Game | Team at launch | Time to first launch | What got it there |
|---|---|---|---|
| **Jailbreak** (2017) | 2 people ([Badimo](https://en.wikipedia.org/wiki/Alex_Balfanz)): one programmer (badcc), one designer/artist (asimo3089) | Built after their earlier open-world game *Volt* (2016) | Reached 70,000 concurrent players on day one. They later hired community creators for content updates |
| **Adopt Me!** | Small founding team. Now **Uplift Games**, around 40+ staff ([source](https://akarinohon.com/text/taketori.cgi/en.wikipedia.org/w/index.php%253Ftitle=Adopt_Me%2521&oldid=1067978599)) | n/a | Long-running live service. The team grew only after the game was a hit. It reportedly uses Rojo so a large team can work together ([DevForum](https://devforum.roblox.com/t/integrate-rojo-into-roblox-studio-officially/657577)) |
| **DOORS** (2022) | 3 people ([LSPLASH](https://knowyourmeme.com/memes/subcultures/roblox-doors)) | About 17 months (Mar 2021 → Aug 2022) | A polished horror experience. Passed 3 billion visits ([Pocket Tactics](https://www.pockettactics.com/roblox/doors-visits)) |
| **Grow a Garden** (2025) | 1 person, a 16-year-old ([IBTimes](https://www.ibtimes.co.uk/roblox-top-creators-devex-payouts-2026-1819403)) | **About 3 days** for the first version | Had about 500 concurrent players when Splitting Point partnered in for equity and added **weekly updates**. It then grew to a 22.3M concurrent peak ([GamesBeat](https://gamesbeat.com/janzen-madsen-interview/)) and reportedly made $12M in May 2025 alone ([RNZ/ODT](https://www.odt.co.nz/entertainment/gaming/millions-going-mad-nz-made-garden-game-rnz)) |
| **Steal a Brainrot** (2025) | A small group ([RoWatcher](https://rowatcher.com/games/7709344486/steal-a-brainrot)), later with Do Big Studios | Unknown | Rode a meme trend to 20M+ concurrent players. Spawned hundreds of clones, and the developers pursued takedowns ([The Star](https://www.thestar.com.my/tech/tech-news/2026/03/25/robloxs-hit-game-steal-a-brainrot-battles-its-many-imitators)) |
| **99 Nights in the Forest** (2025) | 3 core developers plus 1 artist and 1 animator ([DevForum spotlight](https://devforum.roblox.com/t/creator-spotlight-the-story-behind-99-nights-in-the-forest/4036940)) | **About 3 months**, starting from a week-long game jam | Combined a trending format ("survive N days") with a cozy theme. Kept part counts low for mobile. Weekly updates, each preceded by an "Update Party" playtest with players. Reached a 14M concurrent peak. Now being made into a 20th Century Studios film ([Pryor Cashman](https://www.pryorcashman.com/news/pryor-cashman-client-grandmas-favourite-games-99-nights-in-the-forest-headed-to-the-big-screen)) |

### The recurring pattern

1. **Small core team, clear roles.** Two to five people covering design, programming, and building or modeling. Teams only scale up after a hit.
2. **Ship fast and small.** Grow a Garden took 3 days and 99 Nights took 3 months. DOORS (17 months, polished) is the exception rather than the rule. The 99 Nights team's own advice: *"no developer has a 100% hit rate"*, so keep scope small and move on quickly from ideas that aren't working.
3. **Remix a trend.** 99 Nights = "survive N days" trend + Dead Rails influence + a cozy forest. Steal a Brainrot = a meme. Most hits are remixes of a format already gaining momentum.
4. **Weekly live updates are how games grow.** Splitting Point and 99 Nights both treat weekly updates as essential. Grow a Garden went from 500 to 22M concurrent players *after* weekly updates began.
5. **Mobile first.** Low part, vertex, and instance counts. Client-side prediction with server checks so controls feel responsive.
6. **Playtest by watching.** Observe players who don't know they're being watched, then act on feedback that repeats.
7. **It's a numbers game.** Jandel (Splitting Point) estimates *5–6 good games out of 30–40* he made, roughly a 15% rate of games he considered good. Even skilled creators mostly ship games that don't break out.
8. **There's room for new games.** In Aug 2026, **28% of the top-100 games by hours had launched within the previous 90 days** ([IBTimes](https://www.ibtimes.co.uk/roblox-top-creators-devex-payouts-2026-1819403)). Top spots turn over quickly.

### Typical tooling used by serious teams

- Roblox Studio for building, often with Team Create for builders.
- **Rojo + Git + VS Code** for code ([Rojo workflows](https://rojo.space/docs/v7/workflows/)). Commonly "partially managed": Rojo owns the scripts, Studio owns the world.
- Blender for custom meshes. Wally for packages. Selene and StyLua for linting and formatting.
- Freelancers from Talent Hub or the DevForum, usually paid per task or by revenue share. Scripters are paid the most ([DevForum](https://devforum.roblox.com/t/considering-hiring-a-team/2220571)).

---

## 2. Money: how creators get paid

**From player spending to creator cash** (approximate):

- **Roblox's cut:** in-experience sales (game passes, developer products) pay the creator **70%** of the Robux spent.
- **DevEx conversion:** creators cash out at **$0.0038 per earned Robux** for Robux earned since Sep 5, 2025 ([DevForum](https://devforum.roblox.com/t/incorrect-devex-rate-percentage-update-85-claim-is-not-accurate-%F0%9F%A5%80%E2%98%A0%EF%B8%8F/3920224)). Since Jun 8, 2026, Robux from age-verified US 18+ players in eligible experiences pay **$0.0054** ([Roblox docs](https://create.roblox.com/docs/production/monetization/18-plus-devex-rate)).
- **Net result:** players buy Robux for roughly $0.01–$0.0125 each, so the creator keeps **about 21–27% of what players spend** (**estimate**). The platform's ~70% cut is cited in [The Star](https://www.thestar.com.my/tech/tech-news/2026/03/25/robloxs-hit-game-steal-a-brainrot-battles-its-many-imitators).
- **Cash-out minimum:** **30,000 earned Robux**, about $114 ([Roblox docs](https://create.roblox.com/docs/en-us/production/monetization/developer-exchange)). You also need a DevEx portal account, a tax form (W-9 or W-8), and good standing under the Terms. Secondary sources say the account holder must be 13+ with ID verification ([guide](https://rolearn.dev/guidance/roblox-devex-requirements-2026)).

**Platform-wide payouts are huge but extremely concentrated** (12 months to Jun 30, 2026; [IBTimes](https://www.ibtimes.co.uk/roblox-top-creators-devex-payouts-2026-1819403), [SAYS](https://says.com/my/tech/roblox-creators-earn-1-7-billion-developer-payouts)):

| Group | Average DevEx payout |
|---|---|
| All creators (total) | ~$1.7B, up ~50% from the year before |
| Top 10 | $65.7M each (≈39% of the whole pool) |
| Top 100 | $10.8M |
| Top 1,000 | $1.4M |
| **Median DevEx participant** (of 42,000+) | **~$1,500** |

The median figure only counts creators who already cleared the 30,000-Robux cash-out minimum. Most experiences never do. As of Dec 2023, about 7.9 million experiences had **less than 1,000 hours of total playtime** in a year, while only 526 had more than 10M hours ([Statista](https://www.statista.com/statistics/1373941/roblox-developer-experience-breakdown-hours/)).

**Benchmarks for a game's metrics** (GameAnalytics 2026 Roblox report, Aug 2025–Jul 2026, games with 1M+ monthly players; [summary](https://gamedevreports.substack.com/p/gameanalytics-key-roblox-and-roblox)):

| Metric | Median game | Top 1% |
|---|---|---|
| D1 retention | 10.3% | 22.2% |
| D7 retention | 1.6% | 9.1% |
| D30 retention | 0.5% | 4.7% |
| Session length | 9.8 min | 21.1 min |
| Spend per paying player (yr) | $0.81 | $86.36 |

Only **3.8%** of players spent anything in Roblox games over the year. These benchmarks are for games that already reached 1M monthly players, so a new game's numbers will typically be lower.

---

## 3. What ROI looks like for *this* system

### 3.1 Cost per attempt

| Item | Human-built | AI pipeline (**estimate**) |
|---|---|---|
| Development | $20k–$150k+ for a freelance-built game ([vendor estimate](https://game-ace.com/blog/how-to-hire-the-best-roblox-game-developer/)), or a 3-person team working ~3 months | Model tokens for one full pipeline run: roughly $50–$500, depending on how many fix and playtest loops it needs |
| Studio runner | n/a | Windows cloud VM or a spare PC: roughly $50–$150/mo, shared across all games |
| Launch ads | $100–$500 test budget ([BLOXG guide](https://bloxg.com/how-much-does-roblox-marketing-cost)) | Same: $100–$500, with a hard cap |
| **Total per attempt** | **$20k+** | **≈ $200–$1,000** |

The token cost is my estimate. Measure the real number during M1 (see the roadmap in ARCHITECTURE.md).

### 3.2 Paid ads alone don't pay back. Use them to get ranked

- Third-party benchmarks put Sponsored Experience costs anywhere from $0.01–$0.05 per visit up to ~$0.45 per play ([BLOXG benchmarks](https://bloxg.com/statistics/roblox-advertising-benchmarks)). That range is wide and unofficial.
- Rough value of a player to a *median* game: 3.8% pay × ~$0.81 per payer × ~25% creator share ≈ **$0.008** (**estimate**, mixing platform-wide and per-game medians).
- Even for a top-1% game: 3.8% × $86 × 25% ≈ **$0.80 per player** (**estimate**).
- **Conclusion:** for anything short of a hit, a paid visit costs more than the player is worth. The real job of ads is to **buy a few thousand players fast so Roblox's recommendation system can measure retention**. The Home page drives over 90% of platform traffic ([VentureBeat](https://venturebeat.com/business/roblox-wants-to-improve-discovery-for-its-game-creators)), and it ranks games on engagement, retention, and monetization signals ([Roblox discovery docs](https://create.roblox.com/docs/discovery)). Retention earns free traffic. Ads only start that process.

### 3.3 Portfolio math

Outcomes on Roblox follow a power law, so judge ROI across a **portfolio** of attempts, not one game:

```
break-even rate of success = cost per attempt ÷ average lifetime net earnings of a "success"
```

Illustrative scenarios (**all assumptions**, not predictions):

| If a "success" nets… | At $500/attempt you need… | At $1,000/attempt you need… |
|---|---|---|
| $2,000 (small niche game) | 1 success in 4 attempts | 1 in 2 |
| $20,000 (solid mid-tier) | 1 in 40 | 1 in 20 |
| $200,000 (breakout) | 1 in 400 | 1 in 200 |

Comparison point: an experienced human creator reports ~15% "good" games, but only a fraction of those become breakouts. **Expect AI-made games to have a *lower* hit rate than skilled teams**, at least at first. The system's advantages are lower cost per attempt, faster iteration, and tireless weekly updates. Its weaknesses are taste and originality.

### 3.4 How this changes the architecture

The ROI picture argues for **many cheap attempts plus aggressive doubling down**, not one big bet:

1. **Prototype phase:** build a small game in a proven format with a trend twist. Spend under $50 on tokens.
2. **Soft launch:** run a $50–$100 ad burst. Measure D1, session length, and payer conversion over 3–7 days.
3. **Kill or keep:**
   - **Kill** if D1 is under ~8% or sessions are under ~6 min. Archive it and record what was learned in the KB.
   - **Keep** if D1 is at least ~12% and sessions are at least ~10 min. These thresholds sit around the median of games that reached 1M+ monthly players (**assumed thresholds**; tune them with real data).
4. **Double down:** for kept games, run weekly live-ops updates. Raise the ad budget only while revenue per paid player stays above cost per paid player.
5. **Human taste checkpoint:** a 10-minute review by you before scaling spend on any game. This is cheap and high-leverage.

**Risks to plan for:** clones of your hits (Steal a Brainrot faced hundreds), IP problems if the system copies trending games too closely, moderation of AI-generated content, and Roblox changing payout rules (they changed twice between 2025 and 2026).
