---
layout: default
title: Resources
---
 
{% include nav.html %}
 
Sources, readings, and tools that helped with this project.
 
<div role="group" aria-label="Filter resources by category">
  <button type="button" data-filter="all" aria-pressed="true">All</button>
  {% assign cats = site.data.resources | map: "category" | uniq | sort %}
  {% for c in cats %}
  <button type="button" data-filter="{{ c | slugify }}" aria-pressed="false">{{ c }}</button>
  {% endfor %}
</div>
 
<ul style="list-style:none; padding-left:0;">
{% for r in site.data.resources %}
  <li class="resource" data-category="{{ r.category | slugify }}">
    <a href="{{ r.url }}">{{ r.title }}</a>
    <p>Category: {{ r.category }}. Place: {{ r.place }}.</p>
    <p>{{ r.note }}</p>
    <small>Added by {{ r.added_by }}</small>
  </li>
{% endfor %}
</ul>
 
<script>
document.addEventListener("DOMContentLoaded", function () {
  var buttons = document.querySelectorAll("[data-filter]");
  var items = document.querySelectorAll(".resource");
  buttons.forEach(function (btn) {
    btn.addEventListener("click", function () {
      var wanted = btn.getAttribute("data-filter");
      buttons.forEach(function (b) {
        b.setAttribute("aria-pressed", b === btn ? "true" : "false");
      });
      items.forEach(function (item) {
        var show = wanted === "all" || item.getAttribute("data-category") === wanted;
        item.hidden = !show;
      });
    });
  });
});
</script>
