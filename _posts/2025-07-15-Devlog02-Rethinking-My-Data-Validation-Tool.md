---
title: "DevLog#2: Why I Scrapped My Half-Built Data Validation Platform"
date: 2025-07-15 09:00:00 +0800
categories: [Development, Data Engineering, Dev Log]
tags: [data validation, python app development, ai pair programming, scope creep, technical debt, mvp design, pydantic]
author: Charles Fan
description: "A data architect's honest account of scrapping a half-built data validation platform to build what users actually want: a lightweight Python CLI tool."
image:
  path: /assets/img/posts/Cutting-Scope-Creep-for-a-True-MVP.jpg
  alt: "DevLog #2 – Cutting Scope Creep for a True MVP"
seo:
  title: "DevLog #2 - Rethinking My Data Validation Tool: From Scope Creep to a True MVP"
  description: "A senior data architect shares lessons from building a lightweight Python data validation tool. Discover how scope creep and technical debt reshaped his MVP."
  keywords: "data validation, python app development, ai pair programming, scope creep, technical debt, mvp design, pydantic"
---

## From Ambition to Simplicity: The Origin of This Data Validation Tool

Sometimes the hardest part of building a product isn't the coding—it's knowing when to stop and ask: "Am I building the right thing?"

Two months ago, I was deep in the trenches of **ValidateLite**, my data validation tool, convinced I was 70% done. I had a sleek WebUI, metadata management, and a FastAPI backend. Everything looked promising on paper. Then I stumbled across a Reddit post that changed everything.

### The Wake-Up Call

A frustrated developer was complaining about Great Expectations: "Too complex, too many dependencies. I don't want a 'data quality platform'—I want a 'data validation function'."

That hit me like a cold shower. Here I was, building exactly what this person *didn't* want.

### Why Build a Data Validation Tool?

As a seasoned data architect who'd led Java-based data quality tools before, I thought I understood the problem. **Python data validation** seemed straightforward enough. With AI pair programming on the rise, why not leverage my domain knowledge and let AI handle the coding gaps?

My initial vision was ambitious: a WebUI-based tool with metadata configuration, connection management, rule execution, and result visualization. I chose Streamlit for the frontend and FastAPI for the backend, aiming for something lightweight yet comprehensive.

But "lightweight" quickly became anything but.

### Why It Went Wrong

After two months of development, I realized I'd made four critical mistakes:

1. **Unclear requirements** - I had a PRD but no detailed functional specs. AI filled the gaps by expanding features I never asked for.

2. **Vague design** - Especially around API interfaces, leading to two painful refactors mid-development.

3. **Overestimating AI capabilities** - I lacked experience in driving AI for app development, despite my software engineering background.

4. **Perfectionism killing the MVP** - I added complex features like multi-rule execution for single tables and obsessed over test coverage.

The **scope creep** was real. I'd drifted far from my **Minimum Viable Product** goals.

### The Four Questions That Changed Everything

That Reddit post forced me to ask myself some uncomfortable questions:

- Does my product really need to maintain a metadata layer?
- Is my core engine small and beautiful enough to support different deployment scenarios?
- Is WebUI actually necessary for my target users?
- What's the most valuable part of my product, and is it truly at the center?

Once I asked the right questions, the answers became painfully obvious. My **target audience**—data engineers and analysts—didn't want another platform. They wanted a tool that could validate data with a single command, SQL query, or script.

## The Great Pivot

I made a tough decision: scrap the half-built WebUI version and extract the rule engine as a standalone CLI tool.

But there was a problem. The rule engine was tightly coupled with other modules, especially through ORM models designed for metadata persistence. This violated basic **DDD principles** I knew by heart but had somehow ignored in practice.

> "Technical debt must be paid. I couldn't justify keeping legacy code just to maintain backward compatibility."

I redesigned the interface using a clean schema model in a shared module, refactored twice to internalize configuration management and error handling, and finally achieved a truly independent core module.

## Building an App with Python: Lessons Learned

Working on this **Python app development** project taught me that domain expertise doesn't automatically translate to implementation wisdom. When I lacked confidence in Python project structure, I defaulted to AI suggestions—not always the best approach.

The refactoring process was painful but necessary. I couldn't **manage technical debt** by pushing it to future versions. Clean architecture isn't just academic theory; it's survival for any product that plans to evolve.

Now I have a completed CLI module with comprehensive tests, and I'm close to releasing the first version. The journey from bloated platform to focused tool has been humbling but educational.

## What's Next for the data validation tool

The new **ValidateLite** embodies everything I originally wanted: **lightweight Python data validation** that gets you started in 30 seconds. No complex setups, no YAML configuration files, just straightforward data quality checks.

**Key features in the pipeline:**
- **Pydantic**-powered schema validation
- CLI-first design for developer workflows  
- Minimal dependencies and fast startup
- Extensible rule engine architecture

## The Real Lessons

Two key takeaways from this experience:

**Product direction trumps technical execution.** You can build the most elegant code, but if you're solving the wrong problem, it's worthless. I thought I was building for data engineers, but I was actually building for platform administrators.

**Complete requirements and design are non-negotiable.** **AI pair programming** is powerful, but it amplifies both good and bad decisions. Without clear specifications, AI will gladly help you build the wrong thing very efficiently.

These lessons aren't just about **data validation tools**—they apply to any technical product development. Sometimes the best code you can write is the code you delete.

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

