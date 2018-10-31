<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

![image-title-here](img/logo.png){:class="img-responsive"}
{% seo %}
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

### Blogs

* [AWS SAM .Net Core](blogs/awsSamNetCore.md)
* [Aspnet-core Aws-lambda Serverless](blogs/aspnetCoreAwsLambdaServerless.md)
* [Docker tutorial](blogs/dockerFundamentals.md)
* [Quick Enzyme TDD](blogs/enzymeTDD.md)
* [Quick Jest TDD](blogs/jestTDD.md)
* [Jest vs Mocha](blogs/jestVSmocha.md)
* [Keeping Secrets](blogs/keepingSecrets.md)
* [Test Quality](blogs/testQuality.md)
* [Pair Programming](blogs/pairProgramming.md)
* [Migrate repository from TFS to Github](blogs/migrateRepoFromTfsToGithub.md)