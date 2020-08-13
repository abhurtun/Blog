<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
.dropbtn {
  background-color: #4CAF50;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 350px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}
.pad a {
margin-right:20px
}

.dropdown-content a:hover {background-color: #ddd;}

.dropdown:hover .dropdown-content {display: block;}

.dropdown:hover .dropbtn {background-color: #3e8e41;}
</style>

</head>

<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

![image-title-here](img/logo.png){:class="img-responsive"}
{% seo %}

# Welcome

## Hope you enjoy your read.
## Dont be afraid to fail!!!

{{ site.time | date_to_long_string }}
<div class="pad">
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

<div></div>
<div class="dropdown">
  <button class="dropbtn">Blogs</button>
  <div class="dropdown-content">
    <a href="blogs/trunkBasedDevelopment.html">Trunk Based Development</a>
    <a href="blogs/managingCrossTeamDependencies.html">Managing Cross Team Dependencies</a>
    <a href="blogs/goodTechLead.html">Good Tech Lead</a>
    <a href="blogs/debugAWSLambda.html">Debug AWS Lambda using VsCode</a>
    <a href="blogs/awsSamNetCore.html">AWS SAM .Net Core</a>
    <a href="blogs/aspnetCoreAwsLambdaServerless.html">Aspnet-core Aws-lambda Serverless</a>
    <a href="blogs/dockerFundamentals.html">Docker tutorial</a>
    <a href="blogs/enzymeTDD.html<">Quick Enzyme TDD</a>
    <a href="blogs/jestTDD.html">Quick Jest TDD</a>
    <a href="blogs/jestVSmocha.html">Jest vs Mocha</a>
    <a href="blogs/keepingSecrets.html">Keeping Secrets</a>
    <a href="blogs/testQuality.html">Test Quality</a>
    <a href="blogs/pairProgramming.html">Pair Programming</a>
    <a href="blogs/migrateRepoFromTfsToGithub.html">Migrate repository from TFS to Github</a>
    <a href="blogs/awsECSDocker.html">AWS ECS and Docker Quick Guide</a>
  </div>
  <a class="dropbtn" href="/Blog/feed.xml" target="_blank">RSS</a>
</div>