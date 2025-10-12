---
title: "The Real Mess Behind Your IFRS 17 Data Architecture"
date: 2025-10-02 10:00:00 +0800
categories: [Data Architecture, Financial Technology, Organizational Change]
tags: [IFRS 17, data architecture, financial reporting, insurance accounting, data governance, legacy systems, actuarial systems, subledger, data transformation, organizational change, tech debt, data quality, financial systems, regulatory compliance, data engineering, financial technology, business transformation, data platform, financial architecture, digital transformation, compliance, data lineage, data silos, financial data, insurance data, financial analytics]
author: Charles Fan
description: "Your IFRS 17 data project is struggling because you're trying to solve a people problem with a tech solution. Discover why legacy systems, organizational politics, and trust issues are the real challenges."
image:
  path: /assets/img/posts/IFRS_17_Data_Architecture_challenge.jpeg
  alt: "The Real Mess Behind Your IFRS 17 Data Architecture"
seo:
  title: "The Real Mess Behind Your IFRS 17 Data Architecture | Plain Talk Data"
  description: "Your IFRS 17 data project is struggling because you're trying to solve a people problem with a tech solution. Discover the real challenges."
  keywords: "IFRS 17, data architecture, financial reporting, insurance accounting, data governance, legacy systems, actuarial systems, subledger, data transformation, organizational change, tech debt, data quality, financial systems, regulatory compliance, data engineering, financial technology, business transformation, data platform, financial architecture, digital transformation, compliance, data lineage, data silos, financial data, insurance data, financial analytics, financial systems, data platform, financial architecture"
---


In my [last piece](/posts/IFRS17-Data-Quality/), we established that data quality issues are really architectural problems in disguise. But what if the architectural problems are also just a symptom of something deeper? Your IFRS 17 data project is struggling for a simple reason: you're trying to solve a people problem with a tech solution.

The core challenge of implementing IFRS 17 isn’t technical; it’s the collision between your company’s unique history of tech debt and a rigid, one-size-fits-all regulatory mandate. Asking for an IFRS 17 "best practice" is like asking for the best way to renovate an old house without knowing where the load-bearing walls are. Every company’s walls are in a different place.

Let's break down why this is such a tangled mess.

### Your Legacy Systems Aren’t Going Anywhere

Why is every insurer’s data landscape so wildly different? It’s not about good or bad choices. It’s about the irreversible path you’ve walked for decades.

Maybe your company went all-in on SAP back in the 90s, and every process now has a distinct German accent. Another firm might be running on an Oracle finance core bolted to a homegrown underwriting system built when dial-up was still a thing. A third could be in the middle of a post-merger nightmare, trying to stitch together three different generations of technology.

These aren't differences in "maturity." They are fundamental differences in topology, carved out over time. Your company's data flows weren't designed; they were eroded into existence, like a river carving a canyon. You can’t just decide to move the river.

### Your Actuarial Platform Is the Real Boss

The diversity of actuarial modeling platforms gets us closer to the heart of the problem. Your IT architects may think they’re in charge of data architecture, but they’re not. The actuaries are.

The platform they use dictates everything:
*   **Prophet** organizes the world around "Model Points"—statistical bundles of similar policies.
*   **AXIS** often thinks at the individual "Policy" level.
*   **SAS for IFRS 17** tries to define the entire data universe, leaving your data architect as more of an implementer than a designer.
*   **SAP’s FPSL & PaPM** don’t care what your actuarial model does, as long as it feeds them data in the precise format and granularity they demand. They control the architecture from the other end.
*   A **homegrown platform** is a perfect reflection of your chief actuary’s worldview, codified into software.

The uncomfortable truth is this: your data architecture isn't being designed. It’s being dictated, in reverse, by the tools your actuaries chose years ago.

### The Subledger Is a Bad Translator

The subledger system sits in a critical position. It’s supposed to be the universal translator between the languages of business operations, accounting, and the new IFRS 17 standard.

The problem is, these languages aren’t just different; their grammars are incompatible.
*   **Business speaks in:** Policies, endorsements, and claims.
*   **Accounting speaks in:** Debits, credits, and chart of accounts.
*   **IFRS 17 speaks in:** Contractual Service Margins (CSM), cohorts, and loss components.

The subledger tries to map between them, but crucial information gets lost. It’s like trying to write a legal contract using only the vocabulary from a children's picture book. You can point at the right things, but you lose all the essential nuance and structure.

### Data Governance Is Just Office Politics

Why do data governance initiatives always seem to fail? Because data governance isn't about data. It’s about reallocating power.

An IFRS 17 project forces uncomfortable questions out into the open:
*   Who gets to define the official data standard? (The power of definition)
*   Who has the authority to correct historical data? (The power of revision)
*   Who gets the final say on what a piece of data means? (The power of interpretation)

Suddenly, the project becomes a turf war. The actuarial team doesn’t want to give up control over their assumptions. The IT department refuses to be held responsible for the quality of data from systems they don't own. The finance team is deeply uncomfortable relying on data they can’t directly control or audit.

This isn’t a technical challenge. It’s a political one.

### The Fork in the Road: Patch or Rebuild?

When it comes down to it, there are only two real paths for implementing IFRS 17.

**Path A: The Incremental Patch.** You leave the existing legacy systems untouched and build a complex data transformation layer around them. This approach uses technology to paper over the deep-seated organizational problems. It’s a technical fix for a human issue.

**Path B: The Foundational Rebuild.** You use the non-negotiable deadline of IFRS 17 as a lever to force a complete overhaul of your data architecture. This approach uses regulatory pressure to drive long-overdue organizational change.

Your choice between these two paths comes down to a single, fundamental belief: do you think your organization is capable of real change, or can it only adapt at the margins?

### The Impossible Triangle of Implementation

The deepest problem is that every IFRS 17 project is trapped in an impossible triangle. You have three goals:
*   **Compliance:** You must satisfy the regulators.
*   **Accuracy:** Your data must be reliable and correct.
*   **Timeliness:** You must hit the deadline.

Here’s the catch: you only get to pick two.

Most companies, when push comes to shove, choose compliance and timeliness. They sacrifice accuracy. This is why the first year of IFRS 17 reporting is so often a heroic effort of manual adjustments, late nights, and spreadsheet magic.

### You Can’t Code Your Way Out of a Trust Problem

The fundamental dilemma of IFRS 17 data architecture is that we are trying to solve an organizational architecture problem with a technical architecture solution.

The real challenges aren't about designing data pipelines. They are about:
*   How do you get actuaries to share their models and assumptions openly?
*   How do you convince IT to modify a core system that has been running for 20 years without a single hiccup?
*   How do you get your CFO to trust a financial close process based on data they can't see or touch directly?

These are not questions of technology. They are questions of trust.

### So, What Actually Works?

If there’s no "best practice," what’s a realistic path forward? You have to find the path of least resistance within your own organization.

1.  **Map the Real Org Chart.** First, figure out who really controls the data. Ignore the official titles. Who can bring a system to a halt? Start there.
2.  **Triage Your Tech Debt.** Identify which legacy issues absolutely must be fixed for compliance and which ones are merely inefficient. You can’t pay off every debt at once.
3.  **Start with an Easy Win.** Begin with the least controversial data set—often something like earned premiums—to build a small circle of trust and demonstrate value.
4.  **Embrace the Parallel Universe.** Don’t try for a big-bang cutover. Accept the cost and complexity of running new and old systems in parallel for a while.
5.  **Horse-Trade Your Budget.** Use the IFRS 17 budget as a bargaining chip. Offer to solve another department’s long-standing technical pain point in exchange for their cooperation on your project.

But the most critical insight is this: the success of your project depends on your ability to reframe it. Stop calling it a "compliance project" and start calling it a "digital transformation initiative."

If you treat IFRS 17 as a compliance burden, you'll get a patched-up system that barely works. If you treat it as a once-in-a-generation opportunity, it can become the lever that transforms your entire organization.

---

## Recommended Reading

This article is part of a series exploring the multi-layered challenges of IFRS 17 implementation. While this piece focuses on the organizational and political challenges behind data architecture, the broader context involves deeper technical and philosophical issues:

**[IFRS17 Data Quality: A Layered Unraveling of an Architectural Predicament](/posts/IFRS17-Data-Quality/)** - Before diving into organizational solutions, understand the fundamental data quality challenges. This piece reveals that data quality issues aren't just technical problems—they're symptoms of deeper architectural predicaments involving temporal granularity, governance paradoxes, and cognitive chasms between different professional roles.