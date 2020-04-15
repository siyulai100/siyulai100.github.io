---
title: "About"
permalink: /about/
header:
  image: "/images/data.jpg"
---

M.S. in Business Analytics at UCSD, B.A. in Statistics at UIUC

I am a ILLNI and a TRITON!

Extensive experience in Data Manipulation(Python, R, SQL), Statistical Learning, Statistical Computing Methods

Actively seeking for Data Analyst / Product Analyst / Business Analyst position, please contact me freely at Siyu.Lai@rady.ucsd.edu


{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
