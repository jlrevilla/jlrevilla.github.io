---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home

<!-- Loop in you posts -->
{% for post in site.posts %}
  <!-- Here's the header -->
  <header>
    <h2 class="title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
  </header>

  <!-- Your post's summary goes here -->
  <article>{{ post.excerpt }}</article> 
{% endfor %}

---
