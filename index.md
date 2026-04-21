---
layout: default
title: Scratchpad
---

# Scratchpad

A pastebin for bot responses, designs, and notes.

{% assign pastes = site.pages | where_exp: "p", "p.path contains 'pastes/'" | sort: "date" | reverse %}
{% if pastes.size > 0 %}
| Date | Title |
|------|-------|
{% for paste in pastes %}| {{ paste.date | date: "%Y-%m-%d" }} | [{{ paste.title }}]({{ paste.url | relative_url }}) |
{% endfor %}
{% else %}
*No pastes yet.*
{% endif %}
