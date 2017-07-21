![image-title-here](img/logo.png){:class="img-responsive"}
## Welcome to my blog

Hope you enjoy your read.
Dont be afraid to faill!!!

{{ site.time | date_to_long_string }}

### Table of contents

1. [Quick Enzyme TDD](blogs/enzymeTDD.md)
2. [Quick Jest TDD]()
3. [Jest vs Mocha]()
4. [Docker tutorial]()

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

