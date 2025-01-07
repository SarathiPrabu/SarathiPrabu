---
layout: default
title: Home
---

# Welcome to My Blog

This blog is dedicated to summarizing **software engineering topics** for quick reference and sharing my learnings with others. Whether you’re a software enthusiast or someone looking for concise guides, you’ll find valuable insights here.

## About This Blog

Here’s what you can expect:
- **Summaries**: Key concepts in software engineering, presented clearly and succinctly.
- **Problem Solving**: Approaches to real-world problems in programming and beyond.
- **Optimization**: Ideas to streamline workflows and improve solutions.

Feel free to explore the posts and find something that piques your interest.

## About Me

I am a software enthusiast with a professional background spanning:
- **2 years in the Software Industry**: Developing technical solutions and working on programming projects.
- **6 years in the Banking Industry**: Solving operational challenges and improving systems.

In 2022, I moved to the United States to pursue a **Master’s in Computer Science**, reigniting my passion for programming and problem-solving.

## Recent Posts

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

---

Thank you for visiting! Stay tuned for updates, and feel free to share your feedback.
