---
layout: page
permalink: /publications/
title: Publications
description: Publications by categories in reversed chronological order. * denotes equal contribution.
years: [2026,2025,2024,2023,2022]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  <br>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
