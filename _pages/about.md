---
permalink: /
title: "Xuan Luo (罗炫)"
author_profile: true
---

Xuan Luo (罗炫)

I am a PhD student at UC Santa Barbara. My current research is mainly about efficient large language models and applications of generative models.

- github: https://github.com/luoxuan-cs
- huggingface: https://huggingface.co/xuan-luo
- google scholar: https://scholar.google.com/citations?user=z5pKzAcAAAAJ&hl

## Selected publications

{% include base_path %}
{% assign selected_pubs = site.publications | where_exp: 'p', 'p.selected == true' %}
{% if selected_pubs.size > 0 %}
{% for post in selected_pubs reversed %}
{% include archive-single.html %}
{% endfor %}
{% else %}
{% for post in site.publications reversed limit: 5 %}
{% include archive-single.html %}
{% endfor %}
{% endif %}
