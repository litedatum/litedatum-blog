---
title: "DevLog #2 - Rethinking My Data Validation Tool: From Scope Creep to a True MVP"
date: 2025-07-15 09:00:00 +0800
categories: [Development, Data Engineering, Dev Log]
tags: [data validation, python app development, ai pair programming, scope creep, technical debt, mvp design, pydantic]
author: Charles Fan
description: "Lessons learned from building a lightweight Python data validation tool. How scope creep and technical debt reshaped the MVP, and why a CLI-first, testable core won out."
image:
  path: /assets/img/posts/Cutting-Scope-Creep-for-a-True-MVP.jpg
  alt: "DevLog #2 – Cutting Scope Creep for a True MVP"
seo:
  title: "DevLog #2 - Rethinking My Data Validation Tool: From Scope Creep to a True MVP"
  description: "A senior data architect shares lessons from building a lightweight Python data validation tool. Discover how scope creep and technical debt reshaped his MVP."
  keywords: "data validation, python app development, ai pair programming, scope creep, technical debt, mvp design, pydantic"
---

## From Ambition to Simplicity: The Origin of This Data Validation Tool

Have you ever seen a data engineer spend four hours manually checking data quality? Or watched a business analyst lose faith in their dashboard because of a single broken pipeline? I have—and it’s painful to watch.

That’s why I started building **this data validation tool**—lightweight, Python-first, and aimed at people like us. But here’s the thing: the journey didn’t go as planned.

This post is about the messy middle—why my original design spiraled out of control, how I course-corrected, and what I learned about **building an MVP**, **scope creep**, and **technical debt management** along the way.

---

##  Why Build a Data Validation Tool?

As a seasoned data architect, I’ve led teams developing Java-based data quality management systems. So, I’m no stranger to the complexities of data validation.

But this time was different. Instead of leading a team, I wanted to see if I could **build an entire app myself**—in Python. I had never developed a Python application from scratch, but the rise of **AI pair programming** made me wonder:

> *“If I understand the domain, design, and engineering principles, could AI help me bridge the coding gap?”*

Spoiler: yes, but only after a few painful missteps.

---

##  How Scope Creep Killed My First Prototype

The original plan for this data validation tool was ambitious. It was a **web-based data quality solution** featuring:

* **Metadata configuration UI**
* **Connection management**
* **Rule authoring and execution**
* **Results visualization**

For “lightweight” purposes, I chose **Streamlit** for the frontend and combined it with a FastAPI backend, a rules engine, and metadata persistence.

Here’s where I went wrong:

- ✅ I understood **architecture**
- ❌ But I underestimated **development effort**
- ❌ And overestimated **AI’s ability to make design decisions**


Two months later, I had:

* Basic development done
* 60% unit test coverage
* An MVP… that wasn’t minimal at all.

###  My Four Big Mistakes

1. **Vague requirements.**
   I had a PRD but no detailed functional specs. AI filled the gaps, but in unpredictable ways.

2. **Weak design.**
   Especially at the API level. This forced me to refactor—twice.

3. **Blind faith in AI.**
   Pair programming is powerful, but it’s not magic. You still need to *drive* the process.

4. **Perfectionism.**
   I over-engineered features (like multi-rule execution) and obsessed over test coverage—losing sight of my MVP goal.

---

##  The Reddit Post That Changed Everything

One night, I stumbled across a Reddit thread:

> *“I don’t want a data quality platform. I just want a data validation function.”*

That hit me hard. Was I building the wrong thing?

I asked myself:

1. Do I really need a full metadata management layer?
2. Is my core small and elegant enough for flexible deployment?
3. Does my target user want a WebUI? Or a **CLI tool**?
4. What’s the *most valuable* part of this product?

The answer was clear. I was chasing the wrong vision.

---

##  The Hard Reset: Stripping to the Core

I scrapped the half-finished web app. Painful, yes—but necessary.

I focused all energy on:

- ✅ A **rules engine** that was small, fast, and testable
- ✅ A **CLI** interface for quick validation workflows
- ✅ Removing tight coupling with metadata models

This wasn’t easy. The rules engine was deeply entangled with ORM models from the previous design. Untangling them took two major refactors.

I redesigned the `shared` module, created new schema models for the rules engine, and tightly integrated configuration and error handling. Now, the core is **independent and portable**.

The result?
- lightweight CLI-based data validation tool
- Almost 100% test coverage
- A product much closer to my original vision


---

##  Lessons Learned from the Project

This journey taught me two key lessons:

1. **Product direction matters more than technical details.**
   If you get this wrong, no amount of perfect code can save you.

2. **Define requirements and designs upfront.**
   AI pair programming is powerful, but it needs clear boundaries to avoid **scope creep**.

Now I can say with confidence:

> *“I may not know if I’m 100% on the right path, but at least I’m walking in the right direction.”*

---

##  What’s Next?

The CLI module is almost ready for release. In my next DevLog, I’ll share how I designed the **data validation API** and why I kept it **Pydantic-first** to simplify Python data validation workflows.

---

###  SVG Flowchart: ValidateLite’s Direction Reset


<svg width="600" height="400" xmlns="http://www.w3.org/2000/svg">
  <style>
    .box { fill: #e0f2f1; stroke: #00695c; stroke-width: 2; }
    .text { font-family: Arial, sans-serif; font-size: 14px; fill: #004d40; }
    .arrow { stroke: #004d40; stroke-width: 2; fill: none; marker-end: url(#arrowhead); }
  </style>
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7"
            refX="10" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#004d40" />
    </marker>
  </defs>

  <rect x="50" y="20" width="305" height="50" class="box" />
  <text x="60" y="50" class="text">Initial Plan: WebUI + Metadata + Rules Engine</text>

  <line x1="200" y1="70" x2="200" y2="120" class="arrow" />
  <rect x="50" y="120" width="305" height="50" class="box" />
  <text x="60" y="150" class="text">Problems: Scope Creep, Tight Coupling</text>

  <line x1="200" y1="170" x2="200" y2="220" class="arrow" />
  <rect x="50" y="220" width="305" height="50" class="box" />
  <text x="60" y="250" class="text">Decision: Hard Reset & Focus on CLI</text>

  <line x1="200" y1="270" x2="200" y2="320" class="arrow" />
  <rect x="50" y="320" width="305" height="50" class="box" />
  <text x="60" y="350" class="text">Current: Lightweight, Testable Core</text>
</svg>

