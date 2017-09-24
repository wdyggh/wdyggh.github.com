---
layout: default
title: "分类"
nav: true
weight: 1
---
<ul class="list-unstyled">
{% for cat in site.categories %} 
    {% if cat[0] != 'blog' %} 
   <a name="{{ cat[0] }}"></a>
   <h2>{{ cat[0] }}({{ cat[1].size }})</h2> 
     {% for post in cat[1] %} 
    <li><h4>
    <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a>
        <div class="post-date">
          Viewed: <span data-hk-page="{{ post.url | prepend: site.url }}"> - </span> times 
          <!-- {{ post.url | prepend: site.url }} -->
        </div>
    </h4></li>

    {% endfor %} 
   {% endif %} 
{% endfor %} 
</ul>
