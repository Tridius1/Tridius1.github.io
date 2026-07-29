---

layout: page
---

<!-- Flexbox Container -->
<div style="display: flex; align-items: center; gap: 20px; margin-bottom: 30px;">
  
  <!-- Avatar -->
  {% if site.author.avatar %}
    <img src="{{ site.author.avatar | relative_url }}" 
         alt="{{ site.author.name }}" 
         style="width: 100px; height: 100px; border-radius: 50%; object-fit: cover; flex-shrink: 0;">
  {% elsif site.avatar %}
    <img src="{{ site.avatar | relative_url }}" 
         alt="{{ site.name }}" 
         style="width: 100px; height: 100px; border-radius: 50%; object-fit: cover; flex-shrink: 0;">
  {% endif %}

  <!-- Bio and Name -->
  <div>
    <p style="margin: 0; color: #666; font-size: 1.1em; line-height: 1.4;">
      {{ site.author.bio | default: site.description }}
    </p>
  </div>

</div>

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