---
title: "DevLog #1 - ValidateLite: Building a Zero-Config Data Validation Tool"
date: 2025-06-24 09:00:00 +0800
categories: [Development, Data Engineering, Dev Log]
tags: [data validation tool, CLI tools, data quality, zero config, cross-cloud, SQL rule engine, lightweight tools, devlog]
author: Charles Fan
description: "Building ValidateLite: A lightweight, zero-config data validation tool for data engineers and analysts. Get reliable data quality checks running in 30 seconds with code-first approach."
image:
  path: /assets/img/posts/Devlog01-cover.jpg
  alt: "DevLog #1 - Building a Data Validation Tool"
seo:
  title: "DevLog #1 - ValidateLite: Building a Zero-Config Data Validation Tool"
  description: "Learn how I'm building a lightweight data validation CLI tool with zero configuration, 30-second setup, and cross-cloud compatibility. From MVP to production-ready."
  keywords: "data validation tool, lightweight data quality, CLI data validation, 30 second data validation setup, zero config data quality tool, cross-cloud data validation CLI, data quality automation, SQL rule engine, pluggable data validation"
---


> *Cross-cloud ready, code-first, up and running in 30 seconds*

Have you ever seen a data engineer spend four hours manually checking data quality? Or watched a business analyst lose faith in their dashboard due to unreliable data? I have, and it’s tough to witness.

That’s why I’m creating a new **data validation tool**—lightweight, code-first, and designed to get you started in just 30 seconds. No cumbersome frameworks, no complicated setups, just straightforward data quality checks that truly work.

## The Problem: Poor Data Quality is Wasting Our Time

Let’s face it: here’s what’s really going on in data teams:

- **Data engineers** waste over four hours each day on manual data quality checks
- **Business analysts** doubt every insight because of inconsistent data
- **System admins** are jolted awake at 3 AM by data pipeline failures
- **Compliance teams** uncover data quality issues during audits

Current data validation tools either demand a PhD in configuration or require you to overhaul your entire system. We needed something different—a data validation tool that seamlessly integrates into your workflow.

## ValidateLite: An Open Source Data Validation Tool

### The "30-Second" Philosophy

This data validation tool is built on a simple principle: **"Cross-cloud ready, code-first, operational in 30 seconds."** And importantly, it will be open source.

Here's what that means in practice:

### Zero-Config Startup

```python
validate(connection, rules)  # That's it.
```

No YAML hell. No framework lock-in. Just point it at your data and define your rules.

### Framework Independence

We're not marrying you to Airflow, Spark, or any other heavyweight. This data validation tool plays nice with your existing tools - whether that's pandas in a Jupyter notebook or a simple shell script.

### Everyday Integration

Built for the tools you already use:

- Pandas DataFrames ✓
- CSV/Excel files ✓
- Database connections ✓
- Shell automation ✓

## Architecture: Simple but Scalable

A good data validation tool needs clean architecture. We use a three-layer approach:

```
CLI → Core → Shared
```

### The Core: Rule Engine

The heart of any effective data validation tool is its rule engine. It's designed around high cohesion and loose coupling principles - fancy words for "it works well and doesn't break easily."

Key features:

- **Smart query optimization**: Multiple rules on the same table? We merge them into a single query, cutting database calls by 80%
- **Pluggable design**: New data sources or rule types? Just implement the interface
- **Rule type registry**: Adding new validation rules takes 3 steps: inherit, implement, register

### The Shared Layer

Common utilities like database connections, schema definitions, and shared classes live here. Think of it as the foundation that everything else builds on.

### The CLI Interface

Our MVP starts with a command-line interface, but the architecture supports future expansion to web UIs, cloud deployment tools, and even SaaS offerings.

## How to validate data with ValidateLite

### Quick Start

```bash
pip install -e .
validate run examples/orders.csv examples/rules.json --report report.json
cat report.json
```

### Docker Deployment

```bash
docker build -t validate-lite:0.1 .
docker run -v $PWD/examples:/data validate-lite:0.1 \
    validate run /data/orders.csv /data/rules.json
```

### The Core Function

Here's the magic happening under the hood:

```python
async def validation_with_rule_engine(connection: str, rules: str):
    """The heart of everything - simple function, powerful results"""
    
    # Parse whatever connection string you throw at it
    connection_schema = await parse_connection(connection)
    
    # Parse rules from CLI args or JSON file
    rule_schemas = parse_rules(rules, table_name)
    
    # Let the engine do its thing
    engine = RuleEngine(rules=rule_schemas, connection=connection_schema)
    raw_results = await engine.execute()
    
    # Return human-readable results
    return format_results(raw_results)
```

## Technical Deep Dive

### Multi-Source Support

A modern data validation tool needs to handle various data sources through a unified interface:

- **Databases**: MySQL, PostgreSQL, SQLite
- **Files**: CSV and Excel (converted to SQLite for SQL execution)
- **Future**: Cloud storage, APIs, streaming data

### What It Validates (MVP Scope)

- **Non-null checks**: Because empty fields break everything
- **Uniqueness**: Duplicate detection made simple  
- **Range validation**: Numbers and dates within bounds
- **Enum compliance**: Categorical data stays in line
- **Date format consistency**: No more "2023-13-45" surprises

### Extensibility Hooks

The schema design includes hooks for future enhancements:

- Multi-table rules
- Cross-database validation
- Custom rule types
- Real-time monitoring

## Development Approach: Vibe Coding

I'm using what I call "vibe coding" - documentation-driven development with AI assistance. Write comprehensive test cases, let different AI models interpret and implement, then I review and understand every line.

It's faster than traditional coding, but I still own the architecture decisions and understand the codebase deeply.

## What's Next

This data validation tool is starting simple but thinking big. Version 1 focuses on single-table rules, but the architecture supports:

- Multi-table relationships
- Cross-database validation
- Real-time monitoring
- Web UI and cloud deployment

The goal isn't to replace your entire data infrastructure - it's to make data quality checking so easy that you actually do it.

## Why This Matters

**Data validation shouldn't require a dedicated team and six months of setup.** It should be as simple as running a command and getting actionable results.

That's what I'm building. A tool that respects your time, works with your existing stack, and scales when you need it to.

## The Bigger Picture

Poor data quality isn't just a technical problem - it's a trust problem. When analysts can't trust their data, when engineers spend more time validating than building, when compliance teams find gaps during audits, we're not just losing time. We're losing confidence in our data-driven decisions.

This data validation tool aims to restore that confidence, one validation rule at a time.

---

_Next up: The backstory of why I started this project. Spoiler: it involves why existing tools didn't work for my use case and what led to this architecture._