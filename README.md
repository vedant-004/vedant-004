<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=220&color=0:0b0b10,50:2a0f22,100:e11d74&text=Vedant%20Tyagi&fontColor=ffffff&fontSize=56&fontAlignY=38&desc=ML%20%C2%B7%20Data%20Science%20%C2%B7%20Shipped%20to%20production&descAlignY=60&descSize=20&animation=fadeIn" alt="Vedant Tyagi: ML and data science, shipped to production" width="100%" />

<a href="https://scentarchy.com/finder"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=20&pause=1200&color=F7699F&center=true&vCenter=true&width=780&lines=I+build+ML+systems+and+ship+them+to+real+users;Ranking+quality+measured%3A+95.8%25+precision%405+(held-out+96.1%25);27%2C000%2B+records+cleaned%2C+deduplicated+and+scored;Evaluation+first%3A+every+change+has+a+before+and+after;Try+the+live+demo+below+%E2%80%94+it%27s+the+proof" alt="Typing animation of highlights" /></a>

<br/>

<a href="https://scentarchy.com"><img src="https://img.shields.io/badge/%F0%9F%8C%B8_Live_product-scentarchy.com-e11d74?style=for-the-badge" alt="Scentarchy live site" /></a>
<a href="https://www.linkedin.com/in/vedant-tyagi-6b380325a/"><img src="https://img.shields.io/badge/LinkedIn-vedant--tyagi-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:tyagivedant3846@gmail.com"><img src="https://img.shields.io/badge/Email-tyagivedant3846%40gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
<a href="https://www.leetcode.com/vedanttyagi04"><img src="https://img.shields.io/badge/LeetCode-Knight_%C2%B7_max_1909-FFA116?style=for-the-badge&logo=leetcode&logoColor=white" alt="LeetCode" /></a>

<p>
<b><a href="#-60-second-tour">Try it</a></b> ·
<b><a href="#-results-that-matter">Results</a></b> ·
<b><a href="#-the-ml-and-data-work">ML and data work</a></b> ·
<b><a href="#-how-the-system-fits-together">System</a></b> ·
<b><a href="#-problems-i-solved">Hard problems</a></b> ·
<b><a href="#-skills">Skills</a></b> ·
<b><a href="#-for-recruiters">Hire me</a></b>
</p>

</div>

---

## 👋 Hi, I'm Vedant

I work in **machine learning and data science**, and I like models that people actually use. So I built **[Scentarchy](https://scentarchy.com)**: a live perfume encyclopedia, dupe finder and price guide for India. Its core is a ranking and recommendation system over **27,000+ perfumes**, with real data, real users, an evaluation harness and a production deployment.

Most of my time goes into the parts that decide whether ML works: **messy data, feature design, ranking quality, honest evaluation and explaining results**. I also ship the whole thing, from the pipeline to the page, so a model's output reaches a user instead of staying in a notebook.

> **The fastest way to judge my work is to use it.** Everything below is live and clickable. The code is private because it is a real business, and I am happy to walk through it on a call.

---

## 🚀 60-second tour

Each link is a real, working page.

| Try this | What the model or data does | Why it is interesting |
|---|---|---|
| **[🔮 AI Scent Finder](https://scentarchy.com/finder)** | Turns a free-text request or a short wizard into ranked matches with reasons | Weighted note and accord scoring, intent parsing, offline evaluation |
| **[🧬 Find a Dupe](https://scentarchy.com/find-alternative)** | Finds affordable alternatives to a designer perfume | Feature-overlap similarity, with originals ranked before clones |
| **[🌡️ Heat Lab](https://scentarchy.com/climate)** | Scores how a perfume holds up in Indian heat and humidity | Explainable model for the whole catalogue, with a confidence level |
| **[🎨 Accord Finder](https://scentarchy.com/accords)** | Mix accords (woody + vanilla + fresh spicy) and see matches | Accord-vector matching |
| **[🔎 Search](https://scentarchy.com)** | Type any perfume, house or note | Ranked retrieval, originals before dupes, typo tolerance |
| **[🏆 Awards](https://scentarchy.com/awards)** | Animated awards gala | Editable from an admin panel |
| **[🏷️ Brand portal](https://scentarchy.com/brands)** | Indian houses submit their own listings | Data intake with moderation and an audit trail |

---

## 📊 Results that matter

| | |
|---|---|
| **Finder precision@5: 79.8% → 95.8%** | 110 free-text queries on the full 26,898-perfume catalogue (precision@10: 77.3% → 94.5%); wizard on 39 scenarios: 82.1% → 97.9% |
| **Held-out test split: 96.1% precision@5** | 41 queries kept out of weight tuning. On a separate blind set, the first run scored 92.7% before I fixed what it exposed |
| **Hard-constraint violations: 3.0% → 0.1%** | Results that broke the user's stated constraints (price, gender, "no oud") at top 10 |
| **Finder index memory: 66.8 MB → 17.3 MB** | A leaner representation so the model fits the serverless memory budget |
| **Heat model: 0 default scores** | Before, 1,630 perfumes (6.1%) got a placeholder 50. Now missing data shows "no estimate" and every score carries a confidence level (86% complete, 10.5% partial) |
| **50 of 50 sanity checks pass** | Named perfumes by family, pairwise orderings and invariants for the heat model |
| **11,794 perfumes cleaned and added** | 31 verified parts with expected counts, 2,095 uncertain rows held for review, 141 duplicates skipped |
| **Data-quality audit across 26,898 records** | Exact and near-duplicate detection; 20 exact-name groups and 22 looser groups found |

*These are internal measurements. The finder labels are expert-written rules over catalogue data (price, gender, notes, accords, original or dupe), not user clicks, and missing data counts as "not relevant". The blind-set fixes were made after reading its failures, so 92.7% is the honest blind number. I report that gap on purpose.*

---

## 🧠 The ML and data work

<details open>
<summary><b>🔮 Ranking and recommendation (the AI Scent Finder)</b></summary>

- **Problem framing:** a user describes a scent, a budget and a context. The system must return perfumes that satisfy hard constraints first and then rank by fit.
- **Features:** top, heart and base notes, accord rank and strength, concentration, price, gender, original versus dupe, house.
- **Scoring:** weighted note and accord similarity, with note-family handling and a penalty for thin records so sparse data cannot outrank well-described perfumes.
- **Intent parsing:** handles prices that look like names ("Baccarat Rouge 540" is not a ₹540 budget), reference perfumes ("like X, but cheaper"), negation ("no oud"), brand aliases, typos ("sovage") and Hinglish vocabulary.
- **Explainability:** every result shows the notes and accords that matched.
- **Result:** precision@5 rose from 79.8% to 95.8%, and most of the gain came from parsing and data handling rather than weight tuning, which I measured too.
</details>

<details>
<summary><b>📏 Evaluation methodology</b></summary>

- A 110-query set plus a wizard set, with an **independent judge** that shares no code with the ranker
- **Dev and held-out test splits**, plus a separate blind set, to check for overfitting
- Per-category breakdowns to find the weak spots: Hinglish and house queries scored about 63 precision@5 before and 100 after
- Hard-constraint violation rate tracked next to precision
- A written note of what the numbers are *not*, so nobody over-reads them
</details>

<details>
<summary><b>🌡️ Explainable scoring under uncertainty (Heat Lab)</b></summary>

- A deterministic model combining accords, top/heart/base notes and concentration into "holds on skin" and "stays wearable" scores, plus dry-heat, humid-heat, monsoon and air-conditioned variants
- **Uncertainty is part of the output:** each score has a range and a confidence level, and perfumes with no usable data say "no estimate" instead of a made-up number
- Recovers missing concentration from names and descriptions, and down-weights accords that were themselves derived from notes
- Validated with 50 sanity checks and family-level orderings across the whole catalogue
</details>

<details>
<summary><b>🧹 Data pipeline and quality</b></summary>

- Normalised and merged a 14,030-row research dataset into the live catalogue: cleaned names, matched houses, deduplicated, and **held back 2,095 uncertain rows** instead of guessing
- Idempotent, resumable 31-part import with a verified count after every part
- Explicit handling of missing values (1,295 unknown concentrations, 221 missing genders, flat-only note lists) so gaps don't silently bias rankings
- Near-duplicate detection beyond exact name matches
- Provenance rules: no invented prices, ratings or reviews, and no unlicensed photos
</details>

<details>
<summary><b>📈 Analytics and search data</b></summary>

- Search Console query analysis: found that traffic came from specific brand and product queries with low click-through, then reshaped snippets and pages around price and intent
- Staged release of 11.8k new pages to search engines in waves, with a data-driven schedule
- Value-ordered sitemaps so the most useful pages are crawled first
</details>

---

## 🏗️ How the system fits together

```mermaid
flowchart LR
  S["Raw data<br/>research files, retailer feeds,<br/>brand submissions"] --> C["Clean, match,<br/>deduplicate, hold uncertain rows"]
  C --> F["Features<br/>notes, accords, concentration,<br/>price, house"]
  F --> M["Scoring and ranking<br/>finder, dupes, heat model"]
  M --> E["Offline evaluation<br/>judge, splits, blind set"]
  E -- "iterate" --> M
  M --> P["Production<br/>edge-cached site on Cloudflare"]
  P --> U["Users"]
  U -- "queries, search data" --> A["Analytics and SEO tuning"]
  A --> C
```

**Serving stack, in short:** Next.js 16 on Cloudflare Workers, D1 (SQLite with full-text search) and R2, with one cached HTML copy per URL, a cache epoch for instant invalidation, and a shared memory budget so models and indexes fit in a 128 MB Worker.

---

## 🔥 Problems I solved

<details>
<summary><b>Rankings that looked fine but weren't</b></summary>

Spot-checking looked good, so I wrote an evaluation set and an independent judge. It showed specific failures: a perfume name parsed as a budget, a brand turned into a hard filter, and "no oud" returning oud. Fixing parsing and data handling, not tuning weights, moved the metric from 79.8% to 95.8%.
</details>

<details>
<summary><b>Never faking certainty</b></summary>

The old heat score gave 6.1% of perfumes a default 50. I replaced it with a model that reports a range and a confidence level, and that says "no estimate" when the data isn't there.
</details>

<details>
<summary><b>Growing the catalogue by 75% without poisoning it</b></summary>

Importing about 11.8k records meant cleaning, deduplication and a risk of flooding search engines with thin pages. I split the import into 31 verified parts, held back uncertain rows, capped memory, and released the new URLs in waves.
</details>

<details>
<summary><b>Making models fit a serverless budget</b></summary>

Cut the finder's index from 66.8 MB to 17.3 MB and registered it in a shared memory budget so a 27k-item catalogue runs inside a 128 MB Worker.
</details>

<details>
<summary><b>Production bugs I debugged end to end</b></summary>

A React hydration error that silently reset dark mode, traced to a timezone-less timestamp parsed differently on server and browser, fixed with a single UTC rule and server-side decisions.
</details>

---

## 🧰 Skills

<p>
<img src="https://skillicons.dev/icons?i=python,pandas,numpy,sklearn,tensorflow,pytorch,jupyter,sqlite,postgres,docker,git,github" alt="ML and data tools" />
</p>

| Area | What I use |
|---|---|
| **ML and data science** | Python, pandas, NumPy, scikit-learn, TensorFlow, similarity and ranking, feature engineering, offline evaluation (precision@k, held-out and blind sets), explainable scoring |
| **Data engineering** | Cleaning and deduplication pipelines, idempotent imports with verification, SQL (SQLite and PostgreSQL), full-text search |
| **Shipping to production** | TypeScript, Next.js 16 (React 19), Cloudflare Workers, D1, R2, GitHub Actions, edge caching, admin tooling |
| **Analytics and growth** | Search Console analysis, structured data, sitemap strategy, IndexNow |
| **Fundamentals** | Data structures and algorithms, competitive programming, C++, Java |

I also use AI coding agents (Claude Code) in my workflow, with measured evaluations and PR review around them.

---

## 🏅 Beyond the product

- ⚔️ **LeetCode Knight**, max rating **1909**
- 🏆 **Hackathon winner**
- 🚀 **Pre-finalist, Amazon HackOn Season 5**
- 🌱 Learning: advanced ML (deep learning, NLP), system design and cloud architecture

<p align="center">
<a href="https://leetcard.jacoblin.cool/vedanttyagi04?theme=dark&font=Karla&ext=heatmap"><img src="https://leetcard.jacoblin.cool/vedanttyagi04?theme=dark&font=Karla&ext=heatmap" alt="LeetCode stats" width="48%" /></a>
<a href="https://git.io/streak-stats"><img src="https://streak-stats.demolab.com/?user=vedant-004&theme=dark&hide_border=true" alt="GitHub streak" width="48%" /></a>
</p>

---

## 🤝 For recruiters

| | |
|---|---|
| **Roles I'm looking for** | Machine learning engineer, applied data scientist, ML or data-heavy product engineering |
| **Strongest proof** | Use [scentarchy.com](https://scentarchy.com/finder) for two minutes, then ask me about anything you clicked |
| **I can walk you through** | Feature design, ranking and evaluation methodology, the data pipeline and quality checks, uncertainty handling, and how it was deployed |
| **Source code** | The repository is private because it is a real business. Code samples and a live walkthrough are available on request |

📫 **[tyagivedant3846@gmail.com](mailto:tyagivedant3846@gmail.com)** · **[vedant@scentarchy.com](mailto:vedant@scentarchy.com)** · **[LinkedIn](https://www.linkedin.com/in/vedant-tyagi-6b380325a/)** · **[Instagram](https://instagram.com/vedant_.tyagi)** · **[LeetCode](https://www.leetcode.com/vedanttyagi04)**

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=vedant-004&label=Profile%20views&color=e11d74&style=flat" alt="Profile views" />
</p>
