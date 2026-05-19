---
title: HTSync
description: A web app that helps importers classify products and estimate duties under the U.S. Harmonized Tariff Schedule.
date: 2026-05-19
tags:
---
# [HTSync](https://htsync.us.kg/)

> Classify with confidence. A capstone project that turns a 4,000-page tariff manual into a search box.

## What It Is

HTSync is a web app that helps small importers and customs brokers figure out which U.S. tariff code applies to the goods they're shipping, and how much duty they'll owe.

Every product entering the United States needs a 10-digit **HTS code** (Harmonized Tariff Schedule). Pick the wrong one and you either overpay duties or get hit with penalties at the border. The official lookup tools are clunky and assume you already know the answer. HTSync is built for the people who don't.

## What It Does

- **Smart search** — type a plain-English product description ("leather wallet", "cotton t-shirt", "drone parts") and get the most likely HTS codes back, ranked by relevance
- **AI classification** — for ambiguous items, an AI assistant explains *why* a code fits and what alternatives to consider
- **Duty estimates** — see general, special, and Column 2 duty rates side by side, by country of origin
- **Saved products** — keep a personal library of items you import regularly
- **Shipping intel** — compare U.S. ports of entry by congestion, demurrage cost, and best-fit cargo type

## How It Works

1. **Describe** the product in your own words
2. **Review** the matching tariff codes with full descriptions
3. **Compare** duty rates across origin countries
4. **Save** the right code to your product library for next time

## Under the Hood

A lightweight stack chosen to keep the project fast, cheap, and easy to deploy:

- **FastAPI** for the backend
- **SQLite + FTS5** for full-text search across all 99 HTS chapters
- **OpenAI** for AI-assisted classification on tricky items
- **Vanilla HTML/JS** for the frontend — no build step, no framework bloat

Data comes straight from the USITC's public API and refreshes whenever the official tariff schedule is updated.

## Who It's For

- **Small importers** who can't afford a full-time customs broker
- **E-commerce sellers** sourcing from overseas suppliers
- **Customs brokers** who want a faster lookup tool than the official site
- **Students & researchers** studying trade policy


Our product is hosted live at the website below, try it out for yourself!
---
[Website Link](https://htsync.us.kg/)