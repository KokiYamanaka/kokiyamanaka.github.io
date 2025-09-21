---
title: "AI Agents for Scoring Intangible Assets"
excerpt: "A Prototype System to Standardize Intangible Asset Scoring Across Japan"
collection: portfolio
---


## Table of Contents

1. [Japan’s Many Systems, One Service](#japans-many-systems-one-service)  
2. [Problem: Slow Funding, Slow Startups](#problem-slow-funding-slow-startups)  
3. [Solution: A Platform for Scoring Intangible Assets](#solution-a-platform-for-scoring-intangible-assets)  
4. [Technical Challenges](#technical-challenges)  
5. [Prototype](#prototype)  
   - [System Overview](#system-overview)  
   - [Prototype Input and Processing Flow](#prototype-input-and-processing-flow)  
   - [Components](#components)  
     - [Component 1: Search Result Collection](#component-1-search-result-collection)  
     - [Component 2: Search Result Selection](#component-2-search-result-selection)  
     - [Component 3: Fact-Focused Summarization](#component-3-fact-focused-summarization)  
     - [Component 4: Rubric-Guided Scoring](#component-4-rubric-guided-scoring)  

 

## Japan’s Many Systems, One Service

In Japan, consumers encounter multiple payment systems daily. For example, when buying at a Konbini, the cashier asks which payment method you’d like to use. This feels normal in Japan but unusual in countries like Canada, where everyone typically just uses Google Pay.

For store owners, maintaining integrations for all these systems is costly. This pattern extends to B2G and B2B: pensions lack standardized schemas, and banks must maintain custom parsers; payroll and invoicing formats differ across banks, increasing costs. In contrast, Malaysia’s JAKIM system provides a single centralized halal certification system, demonstrating how “one system” reduces inefficiency.


<img alt="image" src="https://github.com/user-attachments/assets/41a0261d-3d60-46d2-b031-426892053975" />

**Key takeaway:** Japan suffers from “too many systems for one service,” creating delays, costs, and conflicts.

 

## Problem: Slow Funding, Slow Startups

Japan’s startup ecosystem faces slow financing. Credit evaluation for early-stage startups is inefficient because each bank uses its own method for evaluating intangible assets (management quality, founder background, business model, etc.).

This leads to manual, fragmented processes where lending decisions are delayed and inconsistent. A standardized scoring system is needed to speed up decisions and improve objectivity.

 

## Solution: A Platform for Scoring Intangible Assets

The proposed solution is a platform that converts unstructured founder data into a standardized creditworthiness score. For example, a Kansai regional bank assessing a strawberry farm startup could use the platform to automatically gather data and produce a score with breakdowns (e.g., management reliability, organizational strength).

This reduces manual due diligence, speeds up credit committee reviews, and accelerates financing.
<img alt="image" src="https://github.com/user-attachments/assets/43d1472f-aca0-40fa-a02b-67f4ee7f7b65" />

 

## Technical Challenges

1. **Data Gathering:** Searching large volumes of qualitative startup data is costly.
2. **Information Extraction:** Scraping reliable and relevant information from the Japanese web is difficult.
3. **Cultural Alignment:** Japanese banks prioritize reliability over disruptiveness. Imported frameworks (like Bill Payne’s ScoreCard) do not align with local expectations.

 

## Prototype

### System Overview

Prototype agent evaluates a single qualitative factor of a startup (e.g., founder’s coachability) by retrieving and summarizing evidence from the web. The process:

1. Collect search results.
2. Select relevant results.
3. Summarize fact-focused content.
4. Assign rubric-based score.

<img alt="image" src="https://github.com/user-attachments/assets/abe1dd56-3b0a-4fc9-8360-0a0f5e0353d8" />

 

### Prototype Input and Processing Flow

Inputs:

* **Target Organization’s Description** (e.g., “トクイテン農業テクは...”).
* **Scoring Criterion** (e.g., “創業者に創業経験がある場合は+3点”).
* **Evidence Requirements** (e.g., “過去のCEO創業経験を確認できる発言や記録を探す”).

The system runs targeted queries, filters SERPs, extracts content, and generates concise fact summaries. These are then mapped to the scoring rubric for final evaluation.

<img alt="image" src="https://github.com/user-attachments/assets/0dd75175-41a3-4834-bc87-0416765ce626" />



### Diving into the Components

#### Component 1: Search Result Collection

* **Mechanism:** Generate queries using LLMs with explorative and exploitative keywords. Collect SERPs (titles, snippets, URLs).
* **Challenge:** US-pretrained LLMs produce loanwords (“リーダーシップ”) instead of Japanese media phrases (“指導力”). Mapped queries improve relevance.

<img alt="image" src="https://github.com/user-attachments/assets/0936ac27-e8b5-459f-9750-668b9a2c24f8" />

#### Component 2: Search Result Selection

* **Mechanism:** LLM scans snippets to decide which results may contain relevant evidence. Prefers sources like note.com blogs over corporate sites for richer founder insights.
* **Principle:** Query the environment with the least cost — snippets first, not full page scrapes.
* **Best Practice:** Use LLMs strategically where reasoning is required; minimize tokens to reduce cost and latency.

<img alt="image" src="https://github.com/user-attachments/assets/d51843ff-caf7-42e2-a585-46181bd70bf1" />

#### Component 3: Fact-Focused Summarization

* **Mechanism:** Extract main content from selected sources and summarize facts aligned with evidence requirements. Output = concise factual notes.
* **Note:** Production-scale system could use hierarchical chunking for long-range summarization.

#### Component 4: Rubric-Guided Scoring

* **Mechanism:** Compare extracted facts with scoring criteria and assign a score.
* **Challenge:** American LLMs often fail to capture Japanese indirect negative nuances (e.g., “対応が遅い”). Fine-tuned Japanese models are needed.


## Goal
Build a scoring system for startup intangible assets that:
- Reduces manual research  
- Makes investor discussions more objective  
- Speeds up funding across Japan  

## Background
Japan suffers from a **“many systems for one service”** problem.  
- In startup lending, each investor applies a different subjective framework.  
- In personal credit, Japan relies on **three bureaus** (CIC, JICC, KSC), while Canada uses a **single unified score** (300–900).  
- The result: fragmented evaluations, duplicated work, and slower funding.  

## Proof of Concept (PoC)
This PoC demonstrates how AI can **unify fragmented processes into a standardized system**.  
- **Use Case:** Intangible asset scoring for startups  
- **Principle:** Standardization of unstructured data into one comparable score  
- **Benefit:** Faster, more consistent credit evaluation across institutions  

## Broader Implications
The same principle applies wherever unstructured data dominates:  
- **Pension Disbursements:** Japan Pension Service (JPS) provides payment data without a standardized schema.  
  - Every bank must build its own parser and update it repeatedly.  
  - Leads to duplication, delays, and inefficiency.  
- **Solution:** Standardize the data representation once, let all banks share it.  

## Takeaway
AI can help Japan move from “many systems for one service” → **fewer unified systems**, enabling:  
- Reduced inefficiency  
- More objective decision-making  
- Accelerated financing and service delivery  



