# Tesla Twitter Sentiment Mining

Sentiment and emotion analysis of 2,000 tweets about Tesla, built in R and visualized in Tableau. Rather than relying on a single sentiment lexicon, the analysis scores every tweet with **three** (Syuzhet, AFINN and NRC) and tests whether they agree.

**MGIS 650 — Introduction to Data Analytics and Business Intelligence** · Rochester Institute of Technology · Spring 2023 · Prof. Jing Tang
**Team of 4:** Akash Taploo · Sameer Bhattarai · Raj Jasani · Sneha Mondal

---

## Data

Collected through the Twitter API with `rtweet`: 1,000 tweets containing the word "Tesla" from any source, plus 1,000 from the official **@Tesla** handle. Restricted to English, retweets excluded, and deduplicated by `user_id`.

A snapshot from spring 2023. Free Twitter API access has since closed, so the collection step is not reproducible today.

## Method

**Text cleaning** (`tm`, `textstem`) — retweet markers, hashtags, URLs, HTML entities, @mentions, carriage returns and emoji stripped; then lowercasing, punctuation and number removal, English stopwords, task-specific stopwords (`tesla`, `t.co`, `https`, `support`), whitespace normalization, stemming and lemmatization.

**Scoring** — each tweet scored independently by Syuzhet, AFINN and NRC, with NRC additionally classifying across its eight emotions: trust, joy, anticipation, surprise, sadness, fear, anger, disgust.

**Lexicon agreement** — AFINN against Syuzhet, NRC against both, tested by correlation and linear regression rather than assumed.

**Keyword segmentation** — tweets flagged on terms tied to Tesla's revenue lines (delivery, deals, electric, autopilot, battery) and on the four terms that dominated the corpus (price, spi, stock, tsla), then emotion profiles compared across them.

## What it found

**Sentiment is net positive.** Trust is the strongest emotion (0.667), closely followed by anticipation (0.665). The strongest negative emotion, anger, sits at 0.310 — under half of trust — and disgust is lowest at 0.123.

**Price is where the goodwill breaks down.** Across the four dominant keywords, "price" carries both the **highest anticipation of anything measured (1.365)** and the **highest sadness (0.423)**. People are more emotionally invested in Tesla's pricing than in any other topic, and more disappointed by it. That split is the actionable finding.

**The lexicons agree, but not perfectly.** AFINN and Syuzhet correlate positively and significantly (p < 0.009), with visible outliers at both extremes — tweets the two methods score very differently. Running one lexicon alone would have hidden that disagreement.

**Vocabulary.** Most frequent terms: *tsla, price, week, top*. Most positive: *top, free, good, like*. Most negative: *loss, hard, miss, break* — a vocabulary closer to stock trading than to car ownership.

**Where tweets came from.** Over 400 distinct sources, concentrated in Twitter Web App (188) and iPhone (140), then Android (71), with iPad and Mac trailing at 13.

## What's in this repo

| File | What it is |
|---|---|
| `twitter_sentiment_team 2.R` | Full R pipeline: collection, cleaning, three-lexicon scoring, emotion analysis, correlation and regression, word clouds |
| `Twitter Sentiment.twbx` | Packaged Tableau workbook — emotion bar charts, favorite-count bubbles, source treemap, word cloud |
| `Twitter Sentiment Project - Team 2.pdf` | 12-page write-up with findings and charts |
| `TSLA_data_2023.csv` | The collected tweet dataset |

## Tools

R (`rtweet`, `syuzhet`, `tidytext`, `tm`, `textstem`, `wordcloud`, `ggplot2`, `reshape2`) · Tableau

## Note

Academic coursework, completed May 2023 as a four-person team project. Tesla is the subject of the analysis, not an affiliation.
