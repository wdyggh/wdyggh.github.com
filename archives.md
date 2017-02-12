---
layout: default
title: "归档"
nav: true
weight: 3
---

<h3> 一共有<span>{{site.posts.size}}</span>篇日志啦.</h3>

<ul class="list-unstyled">
    {% for post in site.posts limit:100 %} 
    {% unless post.next %} 
    <h2>{{ post.date | date: '%Y' }}</h2> 
    {% else %} {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %} {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %} 
    {% if year != nyear %} 
    <h2>{{ post.date | date: '%Y' }}</h2> {% endif %} 
    {% endunless %} 
    <li>
        <h4><span>{{ post.date | date_to_string }}</span>&raquo;<a href="{{ post.url }}">{{ post.title }}</a>
        <div class="post-date">Viewed: <span data-hk-page="{{ site.url }}{{ post.url }}"> - </span> times 
        </div>
        </h4>
    </li> 
    {% endfor %} 
</ul> 
