---
layout: default
title: "Tags"
nav: true
weight: 2
---


<ul class="tag_box inline">
  {% assign tags_list = site.tags %}
    {% for tag in tags_list %} 
      <li><a href="{{ site.baseurl }}{{ tags.html }}#{{ tag[0] }}">{{ tag[0] }} <span>{{ tag[1].size }}</span></a></li>
    {% endfor %}
</ul>

<!-- <div class="div_tag"> -->
<div>
{% for tag in site.tags %} 
	<a name="{{ tag[0] }}"></a><h3>{{ tag[0] }}({{ tag[1].size }})</h3>
	<ul>
	{% for post in tag[1] %}
		<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endfor %}
	</ul>
{% endfor %}
</div>

{% assign tags_list = nil %}



<!-- test -->
<!-- {% for post in site.posts %}
        {% for tag in post.tags %}
          <a class="label" href="{{site.baseurl}}/tags.html"><em>{{ tag }}</em></a>
        {% endfor %}
    {% endfor %} -->


<!-- <script src="/js/react/react.min.js"></script>
<script src="/js/tags.js"></script> -->

<!-- <script type="text/javascript">
// prepare data from jekyll
var $J = {
  // baseUrl: "{{ site.baseurl }}/all-articles/?label=",
  baseUrl: "{{ site.baseurl }}/tags/?label=",
  // staticUrl: "{{ site.static_url }}",
  labels: [
    "显示全部",
    {% for post in site.posts %}
      // {% if post.release %}
        {% for tag in post.tags %}
          "{{ tag }}",
        {% endfor %}
      // {% endif %}
    {% endfor %}
  ],
  posts: [
    {% for post in site.posts %}
      // {% if post.release %}
      {
        title: "{{ post.title }}",
        date: "{{ post.date | date: "%Y-%m-%d" }}",
        link: "{{ post.url | prepend: site.baseurl }}",
        labels: [
        {% for tag in post.tags %}
          "{{ tag }}",
        {% endfor %}
        ]
      },
      // {% endif %}
    {% endfor %}
  ]
};
</script>

<div id="main"></div> -->

<!-- concat React JSX -->
<!-- <script src="/js/react/react.min.js"></script> -->