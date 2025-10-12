---
title: "The Physics of IFRS 17 Data Architecture"
date: 2025-10-11 10:00:00 +0800
categories: [Data Architecture, Financial Technology, Data Engineering]
tags: [IFRS 17, data architecture, event sourcing, bi-temporal data, financial reporting, insurance accounting, data modeling, time-travel, CSM calculation, data quality, atomic layer, semantic layer, financial data, regulatory compliance, data engineering, actuarial systems, financial technology, data governance, temporal data, financial analytics]
author: Charles Fan
description: "Master IFRS 17 data architecture with core engineering principles. Unpack event sourcing, bi-temporal models, and the physics of financial time-travel."
image:
  path: /assets/img/posts/Physics-IFRS17-Data-Architecture.jpg
  alt: "The Physics of IFRS 17 Data Architecture"
seo:
  title: "The Physics of IFRS 17 Data Architecture | Plain Talk Data"
  description: "Master IFRS 17 data architecture with core engineering principles. Unpack event sourcing, bi-temporal models, and the physics of financial time-travel."
  keywords: "IFRS 17, data architecture, event sourcing, bi-temporal data, financial reporting, insurance accounting, data modeling, time-travel, CSM calculation, data quality, atomic layer, semantic layer, financial data, regulatory compliance, data engineering, actuarial systems, financial technology, data governance, temporal data, financial analytics, insurance data, financial systems, data platform, financial architecture"
---

You can’t fix your IFRS 17 data architecture with better technology. You have to fix your organization first. We established that in a [previous discussion](/posts/IFRS-17-Data-Architecture-challenge/), but for those of us in the trenches—the engineers and architects—the conversation eventually has to come back to code and design.

So, let's talk about the hard science of building a data system for this notoriously complex accounting standard. These aren't just best practices; they are principles as unavoidable as the laws of physics.

### Why Two Layers Are Not a Choice, But a Necessity

The classic "atomic" and "semantic" data layers aren't just a matter of design preference. They are a mathematical inevitability dictated by the core of IFRS 17.

Consider the recursive formula for the Contractual Service Margin (CSM):

`CSM(t) = CSM(t-1) + InterestAccretion + NewBusiness - Amortization ± ChangeInEstimates`

This simple-looking equation imposes two rigid requirements on your data system:

1.  **Immutable historical facts:** The state at time `t-1` cannot change.
2.  **Mutable calculation logic:** The logic for `ChangeInEstimates` will definitely change.

If you store facts and logic together, every change in actuarial assumptions would force you to rewrite history. That’s a non-starter. You can't go back in time and change the market interest rate from last quarter just because your model changed today. The only sane solution is to separate the unchangeable past (the atomic layer) from the ever-changing calculations (the semantic layer).

### The True Nature of an Atom

So what, precisely, is an "atom" in this atomic layer?

It's not a policy. It's not a transaction. It's a **state-change event**.

```json
Event = {
    "timestamp": "2025-10-26T10:00:00Z", // Immutable
    "entity_id": "POLICY-12345",
    "event_type": "ENDORSEMENT_ISSUED",
    "payload": { "coverage_change": "+10000" },
    "source_system": "PolicyAdminSuite"
}
```

The critical insight here is that an atom isn't the smallest unit of data; it's the smallest unit of *business change*. Your atomic layer shouldn't store the *current state* of a policy. It must store the *full sequence of events* that led to that state. This is Event Sourcing, tailored for the insurance industry.

### The Computational Heart of the Semantic Layer

If the atomic layer is a ledger of events, the semantic layer is not just "another view of the data." It is the materialization of a **computation graph**.

Every IFRS 17 concept is a node in this graph:

*   **Cohort (Group of Contracts):** A function that aggregates atomic events based on grouping rules.
*   **Fulfillment Cash Flows:** A function that discounts future cash flows using an interest rate curve.
*   **CSM:** A recursive function that operates on the previous CSM and current period changes.

The real challenge is that these nodes are deeply interconnected. The structure is a Directed Acyclic Graph (DAG).

<svg viewBox="0 0 800 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义样式 -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <polygon points="0 0, 10 3, 0 6" fill="#2563eb" />
    </marker>
    
    <filter id="shadow">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-opacity="0.3"/>
    </filter>
  </defs>
  
  <!-- 背景 -->
  <rect width="800" height="200" fill="#f8fafc"/>
  
  <!-- 标题 -->
  <text x="400" y="30" font-family="Arial, sans-serif" font-size="20" font-weight="bold" fill="#1e293b" text-anchor="middle">
    IFRS 17 Dependency Graph (DAG)
  </text>
  
  <!-- 节点: Atomic Events -->
  <rect x="40" y="70" width="110" height="70" rx="8" fill="#3b82f6" stroke="#2563eb" stroke-width="2" filter="url(#shadow)"/>
  <text x="95" y="100" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Atomic
  </text>
  <text x="95" y="118" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Events
  </text>
  
  <!-- 节点: Experience Analysis -->
  <rect x="190" y="70" width="110" height="70" rx="8" fill="#3b82f6" stroke="#2563eb" stroke-width="2" filter="url(#shadow)"/>
  <text x="245" y="100" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Experience
  </text>
  <text x="245" y="118" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Analysis
  </text>
  
  <!-- 节点: Best Estimate Assumptions -->
  <rect x="340" y="70" width="110" height="70" rx="8" fill="#3b82f6" stroke="#2563eb" stroke-width="2" filter="url(#shadow)"/>
  <text x="395" y="95" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Best Estimate
  </text>
  <text x="395" y="113" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Assumptions
  </text>
  
  <!-- 节点: Fulfillment Cash Flows -->
  <rect x="490" y="70" width="110" height="70" rx="8" fill="#3b82f6" stroke="#2563eb" stroke-width="2" filter="url(#shadow)"/>
  <text x="545" y="95" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Fulfillment
  </text>
  <text x="545" y="113" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Cash Flows
  </text>
  
  <!-- 节点: CSM Calculation -->
  <rect x="640" y="70" width="110" height="70" rx="8" fill="#3b82f6" stroke="#2563eb" stroke-width="2" filter="url(#shadow)"/>
  <text x="695" y="100" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    CSM
  </text>
  <text x="695" y="118" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Calculation
  </text>
  
  <!-- 箭头: Atomic Events → Experience Analysis -->
  <path d="M 150 105 L 190 105" stroke="#2563eb" stroke-width="1" fill="none" marker-end="url(#arrowhead)"/>
  <text x="170" y="95" font-family="Arial, sans-serif" font-size="8" fill="#475569" text-anchor="middle">depends on</text>
  
  <!-- 箭头: Experience Analysis → Best Estimate Assumptions -->
  <path d="M 300 105 L 340 105" stroke="#2563eb" stroke-width="1" fill="none" marker-end="url(#arrowhead)"/>
  <text x="320" y="95" font-family="Arial, sans-serif" font-size="8" fill="#475569" text-anchor="middle">depends on</text>
  
  <!-- 箭头: Best Estimate Assumptions → Fulfillment Cash Flows -->
  <path d="M 450 105 L 490 105" stroke="#2563eb" stroke-width="1" fill="none" marker-end="url(#arrowhead)"/>
  <text x="470" y="95" font-family="Arial, sans-serif" font-size="8" fill="#475569" text-anchor="middle">depends on</text>
  
  <!-- 箭头: Fulfillment Cash Flows → CSM Calculation -->
  <path d="M 600 105 L 640 105" stroke="#2563eb" stroke-width="1" fill="none" marker-end="url(#arrowhead)"/>
  <text x="620" y="95" font-family="Arial, sans-serif" font-size="8" fill="#475569" text-anchor="middle">depends on</text>
</svg>

Architecting the semantic layer is really about designing how to efficiently compute, cache, and invalidate parts of this DAG.

### How to Connect to Your Existing Data Platform

Your shiny new IFRS 17 system doesn't live in a vacuum. It has to connect to your existing data landscape, and there are three basic topologies, each with its own physical constraints.

**Model A: The Leech**

<svg viewBox="0 0 800 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义样式 -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <polygon points="0 0, 10 3, 0 6" fill="#2563eb" />
    </marker>
    
    <filter id="shadow">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-opacity="0.3"/>
    </filter>
  </defs>
  
  <!-- 背景 -->
  <rect width="800" height="200" fill="#f8fafc"/>
  
  <!-- 标题 -->
  <text x="400" y="30" font-family="Arial, sans-serif" font-size="20" font-weight="bold" fill="#1e293b" text-anchor="middle">
    Model A: The Leech
  </text>
  
  <!-- 节点: Core Systems -->
  <rect x="30" y="70" width="100" height="60" rx="8" fill="#64748b" stroke="#475569" stroke-width="2" filter="url(#shadow)"/>
  <text x="80" y="95" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Core
  </text>
  <text x="80" y="113" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Systems
  </text>
  
  <!-- 节点: Data Lake -->
  <rect x="170" y="70" width="100" height="60" rx="8" fill="#0ea5e9" stroke="#0284c7" stroke-width="2" filter="url(#shadow)"/>
  <text x="220" y="95" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Data
  </text>
  <text x="220" y="113" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Lake
  </text>
  
  <!-- 节点: IFRS 17 Atomic Layer -->
  <rect x="310" y="70" width="120" height="60" rx="8" fill="#10b981" stroke="#059669" stroke-width="2" filter="url(#shadow)"/>
  <text x="370" y="90" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    IFRS 17
  </text>
  <text x="370" y="108" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Atomic Layer
  </text>
  
  <!-- 节点: IFRS 17 Semantic Layer -->
  <rect x="470" y="70" width="120" height="60" rx="8" fill="#8b5cf6" stroke="#7c3aed" stroke-width="2" filter="url(#shadow)"/>
  <text x="530" y="90" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    IFRS 17
  </text>
  <text x="530" y="108" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Semantic Layer
  </text>
  
  <!-- 节点: Reports -->
  <rect x="630" y="70" width="100" height="60" rx="8" fill="#f59e0b" stroke="#d97706" stroke-width="2" filter="url(#shadow)"/>
  <text x="680" y="105" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Reports
  </text>
  
  <!-- 箭头: Core Systems → Data Lake -->
  <path d="M 130 100 L 170 100" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: Data Lake → IFRS 17 Atomic Layer -->
  <path d="M 270 100 L 310 100" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: IFRS 17 Atomic Layer → IFRS 17 Semantic Layer -->
  <path d="M 430 100 L 470 100" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: IFRS 17 Semantic Layer → Reports -->
  <path d="M 590 100 L 630 100" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 说明文字 -->
  <text x="400" y="165" font-family="Arial, sans-serif" font-size="12" fill="#64748b" text-anchor="middle">
    Least invasive approach, but suffers from accumulated latency
  </text>
</svg>

This is the least invasive approach. But it suffers from accumulated latency, and data quality issues from upstream systems get amplified with each hop.

**Model B: The Twin**

<svg viewBox="0 0 800 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义样式 -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <polygon points="0 0, 10 3, 0 6" fill="#2563eb" />
    </marker>
    
    <filter id="shadow">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-opacity="0.3"/>
    </filter>
  </defs>
  
  <!-- 背景 -->
  <rect width="800" height="200" fill="#f8fafc"/>
  
  <!-- 标题 -->
  <text x="400" y="30" font-family="Arial, sans-serif" font-size="20" font-weight="bold" fill="#1e293b" text-anchor="middle">
    Model B: The Twin
  </text>
  
  <!-- 节点: Core Systems -->
  <rect x="30" y="85" width="100" height="60" rx="8" fill="#64748b" stroke="#475569" stroke-width="2" filter="url(#shadow)"/>
  <text x="80" y="110" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Core
  </text>
  <text x="80" y="128" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Systems
  </text>
  
  <!-- 节点: Data Lake (上方路径) -->
  <rect x="200" y="50" width="100" height="60" rx="8" fill="#0ea5e9" stroke="#0284c7" stroke-width="2" filter="url(#shadow)"/>
  <text x="250" y="75" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Data
  </text>
  <text x="250" y="93" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Lake
  </text>
  
  <!-- 节点: IFRS 17 Atomic Layer (下方路径) -->
  <rect x="200" y="120" width="120" height="60" rx="8" fill="#10b981" stroke="#059669" stroke-width="2" filter="url(#shadow)"/>
  <text x="260" y="140" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    IFRS 17
  </text>
  <text x="260" y="158" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Atomic Layer
  </text>
  
  <!-- 节点: IFRS 17 Semantic Layer -->
  <rect x="370" y="120" width="120" height="60" rx="8" fill="#8b5cf6" stroke="#7c3aed" stroke-width="2" filter="url(#shadow)"/>
  <text x="430" y="140" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    IFRS 17
  </text>
  <text x="430" y="158" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Semantic Layer
  </text>
  
  <!-- 节点: Reports -->
  <rect x="540" y="120" width="100" height="60" rx="8" fill="#f59e0b" stroke="#d97706" stroke-width="2" filter="url(#shadow)"/>
  <text x="590" y="155" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Reports
  </text>
  
  <!-- 箭头: Core Systems → Data Lake -->
  <path d="M 130 100 L 180 80 L 200 80" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: Core Systems → IFRS 17 Atomic Layer -->
  <path d="M 130 130 L 180 140 L 200 150" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: IFRS 17 Atomic Layer → IFRS 17 Semantic Layer -->
  <path d="M 320 150 L 370 150" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: IFRS 17 Semantic Layer → Reports -->
  <path d="M 490 150 L 540 150" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 分支点 -->
  <circle cx="130" cy="115" r="4" fill="#2563eb"/>
</svg>

Here, you create a dedicated, optimized path for IFRS 17. It's faster and cleaner, but now you have a new problem: keeping the twin systems consistent.

**Model C: The Big Bang**

<svg viewBox="0 0 800 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义样式 -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <polygon points="0 0, 10 3, 0 6" fill="#2563eb" />
    </marker>
    
    <filter id="shadow">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-opacity="0.3"/>
    </filter>
  </defs>
  
  <!-- 背景 -->
  <rect width="800" height="200" fill="#f8fafc"/>
  
  <!-- 标题 -->
  <text x="400" y="30" font-family="Arial, sans-serif" font-size="20" font-weight="bold" fill="#1e293b" text-anchor="middle">
    Model C: The Big Bang
  </text>
  
  <!-- 节点: Core Systems -->
  <rect x="30" y="85" width="100" height="60" rx="8" fill="#64748b" stroke="#475569" stroke-width="2" filter="url(#shadow)"/>
  <text x="80" y="110" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Core
  </text>
  <text x="80" y="128" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Systems
  </text>
  
  <!-- 节点: New Central Atomic Layer -->
  <rect x="180" y="85" width="140" height="60" rx="8" fill="#10b981" stroke="#059669" stroke-width="2" filter="url(#shadow)"/>
  <text x="250" y="105" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    New Central
  </text>
  <text x="250" y="123" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Atomic Layer
  </text>
  
  <!-- 节点: Data Lake (上方路径) -->
  <rect x="390" y="50" width="100" height="60" rx="8" fill="#0ea5e9" stroke="#0284c7" stroke-width="2" filter="url(#shadow)"/>
  <text x="440" y="75" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Data
  </text>
  <text x="440" y="93" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Lake
  </text>
  
  <!-- 节点: IFRS 17 Semantic Layer (下方路径) -->
  <rect x="370" y="120" width="140" height="60" rx="8" fill="#8b5cf6" stroke="#7c3aed" stroke-width="2" filter="url(#shadow)"/>
  <text x="440" y="140" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    IFRS 17
  </text>
  <text x="440" y="158" font-family="Arial, sans-serif" font-size="12" font-weight="bold" fill="white" text-anchor="middle">
    Semantic Layer
  </text>
  
  <!-- 节点: Reports -->
  <rect x="560" y="120" width="100" height="60" rx="8" fill="#f59e0b" stroke="#d97706" stroke-width="2" filter="url(#shadow)"/>
  <text x="610" y="155" font-family="Arial, sans-serif" font-size="13" font-weight="bold" fill="white" text-anchor="middle">
    Reports
  </text>
  
  <!-- 箭头: Core Systems → New Central Atomic Layer -->
  <path d="M 130 115 L 180 115" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: New Central Atomic Layer → Data Lake -->
  <path d="M 320 100 L 360 85 L 390 80" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: New Central Atomic Layer → IFRS 17 Semantic Layer -->
  <path d="M 320 130 L 360 140 L 370 150" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 箭头: IFRS 17 Semantic Layer → Reports -->
  <path d="M 510 150 L 560 150" stroke="#2563eb" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
  
  <!-- 分支点 -->
  <circle cx="320" cy="115" r="4" fill="#2563eb"/>
</svg>

This is the purist's choice: rebuild your core data platform around an event-sourced atomic layer that serves everyone. It offers a single source of truth but comes with enormous cost and risk.

Your choice depends on what we might call "data gravity"—a function of your data volume, the number of systems that depend on it, and the cost of changing them.

### A Layered Strategy for Data Quality

"Data quality" isn't a single concept. It means different things at different layers.

At the **atomic layer**, quality means **completeness and immutability**. You're checking if the story makes sense. Did every policy event stream start with a `CREATE` event?

```sql
-- Check for orphaned event chains
SELECT policy_id
FROM events e1
WHERE e1.event_type != 'CREATE'
  AND NOT EXISTS (
    SELECT 1 FROM events e2 
    WHERE e2.policy_id = e1.policy_id 
      AND e2.event_type = 'CREATE'
      AND e2.timestamp < e1.timestamp
);
```

At the **semantic layer**, quality means **consistency and auditability**. You're checking if the math adds up. Does the CSM roll-forward actually balance?

```python
# Check if the CSM roll-forward calculation is balanced
assert abs(
    csm_closing_balance - (
        csm_opening_balance + interest + new_business - amortization + adjustments
    )
) < 0.01
```

The crucial distinction is this: the atomic layer chases *truth*, while the semantic layer chases *correctness*. Truth and correctness are not the same. An endorsement event may have *truly* happened (recorded in the atomic layer), but for IFRS 17 purposes, its financial impact may need to be retrospectively adjusted (handled in the semantic layer).

### The Fundamental Challenge of Time

The deepest technical problem in IFRS 17 is managing multiple, conflicting timelines:

*   **Transaction Time:** When the event actually happened (e.g., a policy was signed on Christmas Day).
*   **System Time:** When the event was recorded in a system (e.g., entered on January 3rd).
*   **Reporting Time:** When the event was included in a financial report (e.g., part of the January close on the 20th).
*   **Effective Time:** When the event's business impact begins (e.g., the policy is effective from January 1st).

Your atomic layer must capture all four. Your semantic layer must be able to reconstruct history from the perspective of any one of them. This is why a **bi-temporal data model** is non-negotiable.

```sql
CREATE TABLE atomic_events (
    -- The business timeline
    valid_from DATE,
    valid_to DATE,
    -- The system's record-keeping timeline
    system_from TIMESTAMP,
    system_to TIMESTAMP,
    -- The event payload
    event_data JSONB
);
```

### The Trade-Off: Computation vs. Storage

The ultimate architectural decision is what to pre-compute and what to compute on the fly. This isn't just about performance; it's a trade-off between **auditability and flexibility**.

*   **Pre-compute more:** Queries are fast, but auditing is a nightmare. The calculation logic is fossilized inside historical data.
*   **Compute on-the-fly:** Auditing is easy because you can re-run any calculation for any point in time, but the performance overhead can be massive.

IFRS 17 is unique because regulators demand that you can prove a historical calculation was based on the assumptions known *at that time*. This leads to a counter-intuitive conclusion: the semantic layer shouldn't store final results. It should store **calculation snapshots**.

```python
class CalculationSnapshot:
    def __init__(self, timestamp, assumptions, formula):
        self.timestamp = timestamp
        self.assumptions = assumptions # A dict of historical assumptions
        self.formula = formula         # The formula string used at the time

    def recalculate(self, atomic_data):
        # Re-run the historical calculation with historical inputs
        return eval(self.formula, {
            'data': atomic_data,
            'assumptions': self.assumptions
        })
```

### An IFRS 17 Version of the CAP Theorem

Every distributed system faces the CAP Theorem—a choice between Consistency, Availability, and Partition Tolerance. IFRS 17 data platforms have their own impossible triangle, especially during the month-end close:

*   **Consistency:** All systems (actuarial, finance, operations) see the same data at the same time.
*   **Availability:** The systems must remain online and usable during the high-pressure closing period.
*   **Partition Tolerance:** The actuarial, finance, and business systems can operate independently without bringing each other down.

During the reporting crunch, you have to sacrifice one. Most organizations choose to **sacrifice Consistency**. This is the technical root of all those late-night "manual journal entries" and post-close adjustments.

### Returning to Engineering Reality

While there is no single "best practice," a few principles are as close to physical laws as you can get:

1.  **Event Sourcing:** The atomic layer must be append-only. No updates.
2.  **Bi-Temporality:** You must separate business time from system time.
3.  **DAG-Based Computation:** The semantic layer's dependencies must not have cycles.
4.  **Idempotency:** Every calculation must be repeatable and yield the same result.
5.  **Snapshot Isolation:** Historical calculations must use historical snapshots of logic and assumptions.

These aren't suggestions. They are the requirements imposed by the mathematical structure of IFRS 17 itself.

Ultimately, the challenge of IFRS 17 data architecture is that you are being asked to build a time-traveling accounting system on top of a tech stack designed for simple create, read, update, and delete operations. This is less an architecture problem and more a physics problem: how do you maintain temporal reversibility in a system that is constantly moving forward?

---

## Recommended Reading

This article is part of a series exploring the multi-layered challenges of IFRS 17 implementation. While this piece focuses on the technical physics of data architecture, the broader context involves organizational and structural challenges that must be addressed first:

**["The Real Mess Behind Your IFRS 17 Data Architecture"](/posts/IFRS-17-Data-Architecture-challenge/)** - Before diving into technical solutions, understand why IFRS 17 projects struggle. This piece reveals that the core challenge isn't technical—it's the collision between your company's unique history of tech debt and a rigid regulatory mandate. You can't code your way out of a trust problem.

**["IFRS17 Data Quality: A Layered Unraveling of an Architectural Predicament"](/posts/IFRS17-Data-Quality/)** - Data quality issues in IFRS 17 aren't just technical problems—they're symptoms of deeper architectural predicaments. This article explores how data governance becomes office politics and why the subledger system is often a bad translator between incompatible business languages.

Together, these three articles form a complete picture: from organizational challenges to architectural principles to the fundamental physics of building time-traveling financial systems. The technical solutions outlined in this article only work when built on the organizational foundation established in the previous discussions.