---
layout: page
title: Categories
---
  <div>
    {% for cat in site.categories %} {% if cat[0] != 'blog' %} 
   <a name="{{ cat[0] }}"></a>
   <h3>{{ cat[0] }}({{ cat[1].size }})</h3> 
   <ul>
     {% for post in cat[1] %} 
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li> {% endfor %} 
   </ul> {% endif %} {% endfor %} 
  </div>