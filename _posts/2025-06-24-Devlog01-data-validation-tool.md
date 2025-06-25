---
title: "DevLog #1: Building a 30-Second Data Validation Tool That Doesn't Suck"
date: 2025-06-24 09:00:00 +0800
categories: [Development, Data Engineering]
tags: [data validation tool, CLI tools, data quality, zero config, cross-cloud, SQL rule engine, lightweight tools, devlog]
author: Charles Fan
description: "Building a lightweight, zero-config data validation tool that gets you from installation to results in 30 seconds. No heavy frameworks, no vendor lock-in - just simple, powerful data quality validation that works with your existing stack."
image:
  path: /assets/img/posts/Devlog01-cover.jpg
  alt: "DevLog #1 - Building a Data Validation Tool"
seo:
  title: "DevLog #1: Building a 30-Second Data Validation CLI Tool | Zero Config Setup"
  description: "Learn how I'm building a lightweight data validation CLI tool with zero configuration, 30-second setup, and cross-cloud compatibility. From MVP to production-ready."
  keywords: "data validation tool, lightweight data quality, CLI data validation, 30 second data validation setup, zero config data quality tool, cross-cloud data validation CLI, data quality automation, SQL rule engine, pluggable data validation"
---

# DevLog #1: Building a 30-Second Data Validation Tool That Doesn't Suck

> *Cross-cloud ready, code-first, up and running in 30 seconds*

Welcome to my first dev log. I'm documenting the journey of building a **lightweight data validation tool** that solves real problems without the enterprise bloat. This post covers the product vision and core architecture - I'll dive deeper into the background story in the next one (trust me, it deserves its own post).

---

## The Problem Is Real, and It's Expensive

Data engineers spend **4 hours daily** manually checking data quality. Business analysts lose trust in their insights because of dirty data. System operators deal with outages triggered by data quality issues. Compliance managers discover quality gaps during regulatory audits.

Sound familiar? Yeah, me too.

## My Solution: Less Is More

I wanted something dead simple that just works. No heavy frameworks, no vendor lock-in, no PhD required to set it up.

### The 30-Second Promise

```bash
# Quick trial
pip install -e .
validate run examples/orders.csv examples/rules.json --report report.json
cat report.json
```

Or if you prefer containers:

```bash
# Production ready
docker build -t validate-lite:0.1 .
docker run -v $PWD/examples:/data validate-lite:0.1 \
    validate run /data/orders.csv /data/rules.json
```

That's it. No configuration files, no database setup, no cluster management.

---

## Architecture: Three Layers, Infinite Possibilities

I built this around a clean **CLI → Core → Shared** separation:

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

### The Smart Parts

**🔧 Pluggable by design**: New data sources or rule types? Just implement the interface and register. Done.

**⚡ Intelligent rule merging**: The engine combines multiple rules for the same table into a single query, cutting database hits by 80%.

**🎯 Zero-config start**: `validate(connection, rules)` and you're running. No YAML hell, no connection pools to configure.

**📱 Future-proof foundation**: CLI today, web UI tomorrow, SaaS eventually. The core stays the same.

### What It Validates (MVP Scope)

- **Non-null checks**: Because empty fields break everything
- **Uniqueness**: Duplicate detection made simple  
- **Range validation**: Numbers and dates within bounds
- **Enum compliance**: Categorical data stays in line
- **Date format consistency**: No more "2023-13-45" surprises

### Data Source Flexibility

Starting with the essentials: **MySQL, PostgreSQL, SQLite**. CSV and Excel files work too (we convert them to SQLite under the hood and run SQL against them).

The **SQL rule engine** speaks SQL dialects, so adding new databases is straightforward.

---

## Development Approach: Vibe Coding with AI

I'm using what I call "vibe coding" - documentation-driven development with AI assistance. Write comprehensive test cases, let different AI models interpret and implement, then I review and understand every line.

It's faster than traditional coding, but I still own the architecture decisions and understand the codebase deeply.

## What's Next

This first version handles single-table rules. **Multi-table validation** and **cross-database rules** are coming - the schema design already has hooks for them.

The CLI is just the beginning. Web UI, cloud deployment tools, maybe even a SaaS offering. The three-layer architecture makes it all possible without rewriting the core.

---

## Why This Matters

**Data validation shouldn't require a dedicated team and six months of setup.** It should be as simple as running a command and getting actionable results.

That's what I'm building. A tool that respects your time, works with your existing stack, and scales when you need it to.

---

## Key Features Summary

✅ **Zero configuration** - Works out of the box  
✅ **30-second setup** - From install to results in half a minute  
✅ **Cross-cloud compatible** - MySQL, PostgreSQL, SQLite, CSV, Excel  
✅ **Pluggable architecture** - Easy to extend with new data sources  
✅ **Intelligent query optimization** - Reduces database hits by 80%  
✅ **Container-ready** - Docker support for production deployments  

---

*Next up: The backstory of why I started this project. Spoiler: it involves why existing tools didn't work for my use case and what led to this architecture.*