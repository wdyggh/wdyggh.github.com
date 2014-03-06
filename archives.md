---
layout: default
title: "Archives"
---
<div>
  <ul>
    {% for post in site.posts limit:100 %}
		{% unless post.next %}
			<h3>{{ post.date | date: '%Y' }}</h3>
		{% else %}
			{% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
			{% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
			{% if year != nyear %}
				<h3>{{ post.date | date: '%Y' }}</h3>
			{% endif %}
		{% endunless %}
		<li><span>{{ post.date | date_to_string }}</span>&raquo;<a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</div>