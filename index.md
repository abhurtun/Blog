<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

![image-title-here](img/logo.png){:class="img-responsive"}
## Welcome to my blog

Hope you enjoy your read.
Dont be afraid to fail!!!

{{ site.time | date_to_long_string }}
<ul class="inlineList">
{% if site.github_username %}
  <li>
    <a href="https://github.com/{{ site.github_username }}">
      <i class="fa fa-github"></i> GitHub
    </a>
  </li>
{% endif %}
{% if site.linkedin_username %}
  <li>
    <a href="https://linkedin.com/in/{{ site.linkedin_username }}">
      <i class="fa fa-linkedin"></i> LinkedIn
    </a>
  </li>
{% endif %}
{% if site.google_plus_username %}
  <li>
    <a href="https://plus.google.com/{{ site.google_plus_username }}">
      <i class="fa fa-google-plus"></i> Google+
    </a>
  </li>
{% endif %}
</ul>

### Table of contents

* [Quick Enzyme TDD](blogs/enzymeTDD.md)
* [Quick Jest TDD](blogs/jestTDD.md)
* [Jest vs Mocha](blogs/jestVSmocha.md)
* [Docker tutorial](blogs/dockerFundamentals.md)
* [Migrate repository from TFS to Github](blogs/migrateRepoFromTfsToGithub.md)