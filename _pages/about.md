---
permalink: /
title: "Jeff Hsu"
excerpt: "Scientist & Researcher"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

## About

I am a scientist interested in genetics, genomics, stem cells and novel paradigm shifting ways to make health care more accessible.

---

## Recent Posts

{% include base_path %}
{% assign recent_posts = site.posts | sort: 'date' | reverse %}
{% for post in recent_posts limit:3 %}
  <article class="archive__item">
    <h3 class="archive__item-title">
      <a href="{{ base_path }}{{ post.url }}">{{ post.title }}</a>
    </h3>
    <p class="archive__item-excerpt">{{ post.date | date: "%B %d, %Y" }}</p>
  </article>
{% endfor %}

[View all posts →](/year-archive/)

---

## Featured Research

### Genetic Control of Left Atrial Gene Expression Yields Insights into the Genetic Susceptibility for Atrial Fibrillation

<img src='/images/genecontrol.jpg' alt='Gene Control Research' style='max-width: 100%; height: auto; margin: 1em 0;'>

Genome-wide association studies have identified 23 loci for atrial fibrillation (AF), but the mechanisms responsible for these associations, as well as the causal genes and genetic variants, remain undefined. To identify the effect of common genetic variants on gene expression that might explain the mechanisms linking genome-wide association loci with AF risk, we performed RNA sequencing of left atrial appendages from a biracial cohort of 265 subjects.

[View all publications →](/publications/)

