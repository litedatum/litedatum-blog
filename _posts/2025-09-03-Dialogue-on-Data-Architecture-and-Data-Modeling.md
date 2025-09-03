---
title: "Data Modeling in Modern Data Architecture: From Layers to Lakehouse"
date: 2025-09-03 20:00:00 +0800
categories: [Data Architecture, Data Engineering, Data Tales]
tags: [data modeling, data architecture, lakehouse, data warehouse, data lake, dimensional modeling, normalized modeling, denormalized modeling, data layers, ODS, data mart, metadata, semantic layer, polymorphic data, Delta Lake, Iceberg, dbt, data lineage, data fidelity, data shareability, data usability, modern data stack, data engineering, data platform, business intelligence, data analytics, data infrastructure, data management]
author: Charles Fan
description: "Is your data architecture stuck in the past? A dialogue on the Lakehouse and future of data modeling—from rigid structures to choreographing data."
image:
  path: /assets/img/posts/Architecture-and-Data-Modeling.jpg
  alt: "Data Modeling in Modern Data Architecture: From Layers to Lakehouse"
seo:
  title: "Data Modeling in Modern Data Architecture: From Layers to Lakehouse"
  description: "Is your data architecture stuck in the past? A dialogue on the Lakehouse and future of data modeling—from rigid structures to choreographing data."
  keywords: "data modeling, data architecture, lakehouse, data warehouse, data lake, dimensional modeling, normalized modeling, denormalized modeling, data layers, ODS, data mart, metadata, semantic layer, polymorphic data, Delta Lake, Iceberg, dbt, data lineage, data fidelity, data shareability, data usability, modern data stack, data engineering, data platform, business intelligence, data analytics, data infrastructure, data management, data transformation, data pipeline, schema-on-write, schema-on-read"
---


Have you ever felt puzzled by this: why does a seemingly simple data request need to traverse through multiple layers—source systems, ODS, data warehouses, data marts—before it can be fulfilled? We're told each layer serves a necessary purpose, but this complexity sometimes feels like historical baggage weighing us down. With the rise of technologies like Data Lakehouse, we can't help but ask: are these layers still necessary? Where is the future of data modeling heading?

To explore these questions deeply, we're going to eavesdrop on a conversation between two leading data architects:

* **Mike**: A seasoned practitioner who believes solid architecture is the foundation of data value. He excels at using vivid analogies to simplify complex technical concepts.
* **David**: A visionary thinker who constantly questions the status quo, explores technological boundaries, and seeks the next paradigm to lead us into the future.

Their intellectual collision will not merely explain "what" data architecture is, but reveal the "why" behind it and envision "what's coming next." Let's step into the conference room.

---

## Chapter 1: The Kitchen Metaphor - Understanding Layered Data Architecture

*The scene opens in a modern conference room at a tech company in Silicon Valley. Two senior data architects, Mike and David, are standing before a whiteboard displaying a layered data architecture diagram: Source Data Layer, ODS (Operational Data Store), Data Warehouse, Data Marts, and Analytics Layer.*

**Mike** (pointing at the whiteboard with enthusiasm): "Look, think of this data architecture like cooking a meal. Your source data layer? That's your raw ingredients—carrots, potatoes, beef—you just wash them clean and store them as-is. The ODS is like your prep station where everything's chopped and ready to go. Then your data warehouse becomes your main kitchen where you combine ingredients following standard recipes, plating everything consistently. And data marts? Those are like different buffet stations—salads here, hot dishes there, desserts over there—so different folks can grab exactly what they need."

**David** (leaning back in his chair, fingers steepled): "The analogy resonates, Mike, but I'm digging deeper here. Why can't we just go straight from raw ingredients to the finished dish? Why do we need all these layers in our data architecture? Each layer must have its own data modeling approach for a fundamental reason, right?"

**Mike**: "Absolutely! See, your source data layer has to stay pristine—it's your only 'evidence room' for tracing back to the truth. Your ODS strips out the noise and standardizes formats, like cutting all those different-sized carrots to the same dimensions. Then your warehouse layer emphasizes consistency and shared dimensions—like making sure every dish follows standard recipes so every customer gets the same taste experience."

## Chapter 2: The Mission-Driven Nature of Data Modeling

**David**: "So the variance in data modeling methods isn't arbitrary—it's dictated by each layer's mission. Source data modeling is about capture and lineage, so it's more normalized, staying close to source systems. ODS modeling focuses on data integration, requiring light consolidation and flexibility. Warehouse modeling serves analytics, so we use dimensional modeling—star schemas, snowflakes—making queries simple and efficient."

**Mike**: "Exactly! And by the time you hit data marts and analytics layers, your data modeling gets really flexible. You can even denormalize, pre-calculate metrics—basically portion out ready-to-serve meals so customers can grab and go."

**David** (standing up, pacing): "This reveals something profound: different layers in data architecture balance three fundamental tensions—data fidelity, shareability, and usability. The closer to source, the more we emphasize preservation. The closer to users, the more we emphasize accessibility. The middle layers control complexity while ensuring shareability."

> *"We're not just designing models—we're designing information flow, ensuring it can trace back to origins while serving decision-making."* - David

**Mike**: "Your insight maps like a spectrum: left to right, data gets progressively 'processed,' and data modeling methods shift from conservative to bold, from normalized to denormalized."

**David**: "Which explains why we can't use uniform data modeling across all layers—we'd lose balance. Either everything stays pure and users suffer, or everything gets simplified and we lose traceability."

> *"Different data modeling approaches are really responses to each layer's 'role definition.' Like using different knives for different cuts—you don't bone a chicken with a paring knife."* - Mike

## Chapter 3: Challenging the Status Quo - Are Layers Still Necessary?

**David** (turning back to Mike): "But here's what keeps me up at night: are these layers even optimal? Are we stuck with this data architecture because of legacy constraints? If technology advances enough—say with Lakehouse architectures—could we merge ODS and warehouses, maybe even analyze directly on source data?"

**Mike**: "You're hitting something real there. Traditional layering was a compromise. Back when storage was expensive, compute was slow, and tools were limited, we needed ODS for cleaning first, then warehouses for performance. Lakehouse is like having one massive pot that can both boil soup and stir-fry—lots of specialized work can merge."

**David**: "So if we can reduce layers, how does data modeling evolve? Do we need to find some unified modeling approach that's both faithful and efficient?"

**Mike**: "In Lakehouse environments, you might have the same physical storage supporting different logical views for different needs: one table is your raw Delta table, another is your cleaned view, a third is your aggregated dimension table."

## Chapter 4: From Physical to Logical - The Future of Data Architecture

**David** (eyes lighting up): "This touches the fundamental question: do we need true physical layering, or just **semantic layering**? Essentially, we're not solving 'where to put it' but 'how to ensure each user type sees the data they need while tracing back to original truth.'"

**Mike**: "Like building a transparent skyscraper: ground floor has raw archives, second floor has organized files, third floor has dashboard views. People move freely between floors instead of hauling boxes between different warehouses."

> *"I suspect future data modeling will emphasize logical over physical layering, using metadata, tags, and version control to maintain lineage and consistency. We're shifting data modeling from 'building structures' to 'defining relationships'."* - David

**Mike**: "Like moving from 'sculpting statues' to 'drawing blueprints'—data can flow and recombine, but blueprints ensure nothing gets lost."

**David**: "So the fundamental reason different layers use different data modeling methods is to keep data in optimal 'form' at each stage. If future technology lets the same data exist in multiple forms simultaneously, we might unify 'multiple data modeling approaches' into one switchable view system."

## Chapter 5: Polymorphic Data - The Technical Reality Check

**David** (challenging): "You talk about 'same data existing in multiple forms,' but how do we actually implement that? Data isn't magic—it's either a raw table or an aggregated table. How can it be both simultaneously?"

**Mike**: "People are already doing this. Technologies like Lakehouse, Iceberg, Delta Lake let you define multiple 'table views' over the same physical storage: one view shows the raw append-only log, another shows cleaned tables, a third shows pre-aggregated materialized views. Users see different 'masks' over the same underlying data."

**David**: "I see—using **metadata layers** and **compute deferral** to handle form switching:
- Metadata records each view's definition and lineage relationships, ensuring traceability  
- Compute layers can generate forms on-demand or use materialized tables for speed  
This is essentially 'Form-as-a-Service.'"

**Mike**: "Right, and modern query engines—DuckDB, Trino, Snowflake—can run SQL directly on raw data, even cache results as different forms. Users don't need to know whether it's storage or computation behind the scenes."

**David**: "But what's the cost? This 'polymorphism' isn't free. Metadata needs real-time sync, view definitions need traceability, compute resources need constant availability—otherwise it becomes 'delayed switching' not 'free switching.'"

## Chapter 6: The Building Blocks of Tomorrow

**Mike**: "Exactly why pioneers are solving these pain points:
- **Delta Lake / Iceberg / Hudi** → ACID transactions and snapshots make multi-view traceability possible  
- **Snowflake / BigQuery** → storage-compute separation enables elastic query granularity switching  
- **dbt** → code-managed views and models make forms versionable and reproducible"

**David**: "So we already have the foundation. The future might be combining these pieces: a unified semantic layer that can declare 'I need this data in raw form' or 'I need it aggregated by business metrics,' with underlying platforms automatically deciding whether to compute, snapshot, or cache."

**Mike**: "Like Photoshop layers—same image, but you can toggle filters on and off without creating new files."

> *"This design transforms the data modeler's role: no longer 'sculptors' but 'choreographers'—defining relationships and transformation rules between various forms, letting data present the right face when needed."* - David

**Mike**: "So 'unifying multiple data modeling approaches into switchable views' isn't utopian—it's the product of **metadata-driven + compute virtualization + storage-compute separation**. We're already at the doorstep."

## Conclusion: Two Visions, One Future

**David** (standing up, looking at the whiteboard): "You know what this means for data architecture as we know it?"

**Mike**: "That we're not just evolving our data modeling techniques—we're fundamentally reimagining how data lives and breathes in the modern enterprise."

> *"The future of data architecture isn't about building better warehouses. It's about creating data ecosystems that are simultaneously archaeological and prophetic—preserving every grain of historical truth while adapting instantly to tomorrow's questions."* - David

---

## Summary of Core Perspectives

**Mike's Core View**: Traditional layered data architecture serves essential purposes, with each layer optimized for specific functions through appropriate data modeling techniques. While new technologies like Lakehouse can consolidate some layers, the fundamental principles of data flow and transformation remain valid. The evolution lies not in abandoning proven patterns but in making them more flexible and efficient.

**David's Core View**: The current layered approach reflects historical constraints rather than optimal design. Future data architecture should emphasize logical over physical separation, with polymorphic data systems that can present multiple forms simultaneously. Data modeling must evolve from creating rigid structures to defining fluid relationships, enabling the same data to serve multiple purposes without duplication.

**The Convergent Conclusion**: Both perspectives point toward a future where data architecture balances preservation with accessibility through intelligent abstraction layers. The key insight is that different data modeling approaches exist not by accident but by design—each serving specific tensions between fidelity, shareability, and usability. The future will likely preserve these distinct purposes while unifying them through metadata-driven, semantically layered systems.

## Key Takeaways

• **Data architecture layers exist to balance three fundamental tensions**: data fidelity (preserving original truth), shareability (enabling cross-functional access), and usability (supporting efficient analysis)

• **Different data modeling approaches are mission-driven, not arbitrary**: source layers use normalized models for lineage, warehouse layers use dimensional models for analytics, and mart layers use denormalized models for performance

• **Modern technologies enable "polymorphic data"**: the same physical data can present multiple logical forms through metadata layers, compute virtualization, and storage-compute separation

• **The future of data modeling shifts from "building structures" to "defining relationships"**: emphasis moves from physical layering to semantic layering, with data modelers becoming "choreographers" rather than "sculptors"

• **Current innovations are building blocks for unified data architecture**: Delta Lake, Lakehouse, dbt, and cloud-native platforms are converging toward "Form-as-a-Service" capabilities that maintain layered benefits without physical complexity