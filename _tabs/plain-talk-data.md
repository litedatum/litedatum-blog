    ---
layout: page
title: Plain Talk Data
icon: fas fa-database
order: 3
---

# Plain Talk Data Series

Welcome to **Plain Talk Data** - where complex data management concepts are explained in simple, everyday language!

## 🎯 What This Series Is About

Data management doesn't have to be intimidating. Whether you're a complete beginner or someone who's heard these terms thrown around but never really understood them, this series breaks down:

- Data governance concepts
- Data engineering methods  
- Analytics terminology
- Cloud data services
- And much more!

## 📚 All Posts in This Series

<div class="post-list">
{% for post in site.categories["Plain Talk Data"] %}
  <div class="post-preview">
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
    <p>{{ post.description | default: post.excerpt | strip_html | truncate: 150 }}</p>
    <div class="post-tags">
      {% for tag in post.tags %}
        <span class="tag">{{ tag }}</span>
      {% endfor %}
    </div>
  </div>
{% endfor %}
</div>

## 🚀 Upcoming Topics

- What is Big Data? (And why should you care?)
- APIs Explained: The Waiters of the Digital World
- Cloud Storage vs. Traditional Storage
- Data Privacy: What Companies Know About You

## 💡 Suggest a Topic

Have a data-related term that confuses you? [Open an issue](https://github.com/litedatum/litedatum-blog/issues) or reach out on social media!

---

<style>
.post-list {
  margin-top: 2rem;
}

.post-preview {
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  background: var(--card-bg);
}

.post-preview h3 {
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.post-preview h3 a {
  text-decoration: none;
  color: var(--heading-color);
}

.post-preview h3 a:hover {
  color: var(--link-color);
}

.post-meta {
  color: var(--text-muted-color);
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.post-tags {
  margin-top: 1rem;
}

.tag {
  display: inline-block;
  background: var(--tag-bg);
  color: var(--tag-color);
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  font-size: 0.8rem;
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}
</style> 