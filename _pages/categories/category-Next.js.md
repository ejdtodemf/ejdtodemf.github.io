---
title: "Next.js"
layout: archive
permalink: categories/Next.js
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['Next.js'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
