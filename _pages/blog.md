---
layout: page
title: Blog
permalink: /blog/
image: profile10.jpg
---


<div class="container">
	<div class="row">
		<div class="col col-12">
			{% if site.posts.size > 0 %}
				<h4 class="lates-title"> Últimas publicaciones </h4>
			{% endif %}
		</div>
	</div>
</div>

<div class="container">
	<div class="row">
	{% if site.posts.size > 0 %}
		{% for post in paginator.posts %}
			{% include article-content.html %}
		{% endfor %}
	{% endif %}
	</div>
</div>

{% include pagination.html %}