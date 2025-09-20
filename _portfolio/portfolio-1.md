---
title: "Automated Quotation for Construction Supplier"
excerpt: "Automated system that converts external construction orders into standardized internal quotations using OCR, vector search, and LLMs."
collection: portfolio
---


### The Problem
Our client is a construction component supplier with over 110 franchise locations across Japan. When construction companies place orders, they submit lists of required components written in their own terms or formats.

The supplier must then manually convert these lists into internal quotation documents by mapping the construction company’s terms to the supplier’s standardized internal product names.

**Construction companies submission :** 
<img src="/images/client_order_.png" alt="Dashboard view" />

**Internal Quotation :** 
<figure>
  <img src="/images/client_quotation.png" alt="Dashboard view" />
  <figcaption><em>Blue = Input | Red = Output</em></figcaption>
</figure>

 

To understand the pain of this problem, employees at the construction supplier used to spend hours manually translating each external product name. They had to search through a physical catalog, guess which internal product it matched, and then write down the correct product name and ID — a slow and error-prone process.

### The Solution
We built an automated pipeline that eliminates the manual quotation process:
1. Input: Construction companies upload their order sheets in CSV or PDF format.
2. OCR + Structuring: Orders are parsed using OCR and cleaned into standardized fields with the help of an LLM.
3. Vector Search: For each external product name, the system retrieves the top-K most similar internal product names and IDs using a vector database.
4. Final Mapping with LLM: These similar matches are passed to an LLM, which selects the most appropriate internal product name and ID for quotation.

### Takeaways
- **Start with first principles** – Don’t over-engineer with multi agent hype or frameworks. After several PoCs, we reduced the system to just 4 core components.
- **Always structure LLM output** – It simplifies downstream logic and avoids errors.
- **Minimize token usage** – Reducing input/output tokens improves latency and keeps the experience snappy.
- **Keep it lightweight** – From architecture to LLM calls, lean systems perform better and scale easier.
