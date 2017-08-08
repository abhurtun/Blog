<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

![image-title-here](img/logo.png){:class="img-responsive"}
## Welcome to my blog

Hope you enjoy your read.
Dont be afraid to fail!!!

{{ site.time | date_to_long_string }}
<div>
{% if site.github_username %}
    <a href="https://github.com/{{ site.github_username }}">
      <i class="fa fa-github"></i> GitHub
    </a>
{% endif %}
{% if site.linkedin_username %}
    <a href="https://linkedin.com/in/{{ site.linkedin_username }}">
      <i class="fa fa-linkedin"></i> LinkedIn
    </a>
{% endif %}
{% if site.google_plus_username %}
    <a href="https://plus.google.com/{{ site.google_plus_username }}">
    <i class="fa fa-google-plus"></i> Google+
    </a>
{% endif %}
</div>

<button data-toggle="collapse" data-target="#blogs">Blogs</button>
<button class="collapse">
<div id="blogs" class="collapse">
    <li>
        <a href="blogs/enzymeTDD.md">
            [Quick Enzyme TDD]
        </a>
    </li>
    <li>
        <a href="blogs/jestTDD.md">
        [Quick Jest TDD]
        </a>
    </li>
    <li>
        <a href="blogs/jestVSmocha.md">
        [Jest vs Mocha]
        </a>
    </li>
    <li>
        <a href="blogs/dockerFundamentals.md">
        [Docker tutorial]
        </a>
    </li>
    <li>
        <a href="blogs/migrateRepoFromTfsToGithub.md">
        [Migrate repository from TFS to Github]
        </a>
    </li>
</div>