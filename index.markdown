---

layout: page
---

<div class="project-grid">
	{% for project in site.projects %}
		<div class="project-card">
			<div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
				{% if project.thumbnail %}
					<img src="{{ project.thumbnail }}" 
						alt="{{ project.title }} icon" 
						style="width: 50px; height: 50px; object-fit: cover; border-radius: 20px; flex-shrink: 0;">
				{% endif %}
				<h3 style="margin: 0;"><a href="{{ project.url }}">{{ project.title }}</a></h3>
			</div>
		<p>{{ project.subtitle }}</p>
		{% if project.github_link %}
			<a href="{{ project.github_link }}">View Code</a>
		{% endif %}
		</div>
	{% endfor %}
</div>