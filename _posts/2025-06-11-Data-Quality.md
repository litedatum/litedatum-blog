---
title: "Plain Talk Data: Data Quality"
date: 2025-06-11 14:00:00 +0800
categories: [Plain Talk Data, Data Management]
tags: [data quality, data validation, data accuracy, data completeness, data governance, beginner, data management]
author: Charles Fan
description: "A plain-English explanation of data quality - the difference between a GPS that works and one that sends you into a lake. Learn the four pillars of data quality."
image: /assets/img/posts/data-quality-cover.jpg
seo:
  title: "What is Data Quality? GPS vs Lake Navigation | Plain Talk Data"
  description: "Understand data quality in simple terms. Learn the four key dimensions of data quality: accuracy, completeness, consistency, and timeliness."
  keywords: "data quality, data validation, data accuracy, data completeness, data consistency, data governance, data management"
---

## Plain Talk Data: Data Quality

**Data Quality = "The difference between a GPS that works and one that sends you into a lake"**

Data quality is making sure your information isn't lying to you, missing important bits, or just plain making stuff up.

---

## Think of It Like Food in Your Fridge

### Good Quality Data = Fresh groceries
- **Customer email:** "john@gmail.com" ✅
- **Order date:** "2024-03-15" ✅ 
- **Phone number:** "555-123-4567" ✅
- **Everything's accurate, complete, and you can actually use it**

### Bad Quality Data = Expired milk and moldy bread
- **Customer email:** "john@@gmailcom" (typo - can't send emails)
- **Order date:** "March sometime" (too vague - can't track trends)
- **Phone number:** "555" (incomplete - can't call them)
- **Address:** "123 Main St, Earth" (useless for shipping)

---

## The Four Big Quality Checks

### 1. Accuracy = "Is this actually true?"
Not listing someone's age as 150 or their zip code as "banana"

**Examples:**
- ✅ Birth date: 1985-03-15
- ❌ Birth date: 2085-03-15 (future baby?)
- ✅ Email: sarah@company.com
- ❌ Email: sarah@companycom (missing dot)

### 2. Completeness = "Are we missing important stuff?"
Like having a customer's name but no way to contact them

**Examples:**
- ✅ Customer record with name, email, phone, address
- ❌ Customer record with just a name (how do you reach them?)
- ✅ Order with product, quantity, price, date
- ❌ Order missing the price (how much did they pay?)

### 3. Consistency = "Does this match everywhere else?"
Don't call the same person "John Smith" in one system and "J. Smyth" in another

**Examples:**
- ✅ Same customer ID across all systems
- ❌ Customer #123 in sales, Customer #456 in billing (same person)
- ✅ Product codes match between inventory and orders
- ❌ "iPhone 15" vs "Apple iPhone 15" vs "IP15" (same product)

### 4. Timeliness = "Is this still current?"
Last year's inventory counts won't help you today

**Examples:**
- ✅ Stock levels updated hourly
- ❌ Stock levels from last month (probably wrong now)
- ✅ Customer preferences from recent surveys
- ❌ Customer preferences from 5 years ago (people change)

---

## Real-World Pain

> **Bad data quality is like following directions from someone who's never been to your destination.** You'll waste time, money, and probably end up somewhere you don't want to be.

### The Cost of Bad Data
- **Marketing campaigns** sent to wrong addresses
- **Inventory decisions** based on outdated numbers
- **Customer service** can't find customer records
- **Financial reports** that don't add up
- **Compliance issues** from inaccurate records

---

## The Bottom Line

**Good data = confident decisions**  
**Bad data = expensive mistakes**

Think of data quality as the foundation of your house. You can build the most beautiful structure on top, but if the foundation is cracked, everything else will eventually fall apart.

---

## Quality Checklist

Before trusting any data, ask yourself:
- [ ] **Is it accurate?** (matches reality)
- [ ] **Is it complete?** (has all necessary fields)
- [ ] **Is it consistent?** (matches other sources)
- [ ] **Is it current?** (recent enough to be useful)

If you can't check all four boxes, proceed with caution - or better yet, fix the data first.
