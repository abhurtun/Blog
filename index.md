<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
/* The sidebar menu */
.sidebar {
  height: 100%; /* 100% Full-height */
  width: 0; /* 0 width - change this with JavaScript */
  position: fixed; /* Stay in place */
  z-index: 1; /* Stay on top */
  top: 0;
  left: 0;
  background-color: #111; /* Black*/
  overflow-x: hidden; /* Disable horizontal scroll */
  padding-top: 60px; /* Place content 60px from the top */
  transition: 0.5s; /* 0.5 second transition effect to slide in the sidebar */
}

/* The sidebar links */
.sidebar a {
  padding: 8px 8px 8px 32px;
  text-decoration: none;
  color: #818181;
  display: block;
  transition: 0.3s;
}

/* When you mouse over the navigation links, change their color */
.sidebar a:hover {
  color: #f1f1f1;
}

/* Position and style the close button (top right corner) */
.sidebar .closebtn {
  position: absolute;
  top: 0;
  right: 25px;
  font-size: 36px;
  margin-left: 50px;
}

/* The button used to open the sidebar */
.openbtn {
  font-size: 20px;
  cursor: pointer;
  background-color: #111;
  color: white;
  padding: 10px 15px;
  border: none;
}

.openbtn:hover {
  background-color: #444;
}

/* Style page content - use this if you want to push the page content to the right when you open the side navigation */
#main {
  transition: margin-left .5s; /* If you want a transition effect */
  padding: 20px;
}

/* On smaller screens, where height is less than 450px, change the style of the sidenav (less padding and a smaller font size) */
@media screen and (max-height: 450px) {
  .sidebar {padding-top: 15px;}
  .sidebar a {font-size: 18px;}
}
</style>

<script>
/* Set the width of the sidebar to 250px and the left margin of the page content to 250px */
function openNav() {
  document.getElementById("mySidebar").style.width = "450px";
  document.getElementById("main").style.marginLeft = "250px";
}

/* Set the width of the sidebar to 0 and the left margin of the page content to 0 */
function closeNav() {
  document.getElementById("mySidebar").style.width = "0";
  document.getElementById("main").style.marginLeft = "0";
}
</script>

</head>

<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

<div id="main">

<img src="./img/logo.png" alt="Arvin Bhurtun" width="250" height="250" align="middle">
 {% seo %}

<h1>Welcome</h1>

<h2>Hope you enjoy your read<h2>

<h3>Dont be afraid to fail!!!</h3>

<div id="mySidebar" class="sidebar">
  <a href="javascript:void(0)" class="closebtn" onclick="closeNav()">&times;</a>
  <a href="blogs/trunkBasedDevelopment.html">Trunk Based Development</a>
  <a href="blogs/managingCrossTeamDependencies.html">Managing Cross Team Dependencies</a>
  <a href="blogs/goodTechLead.html">Good Tech Lead</a>
  <a href="blogs/debugAWSLambda.html">Debug AWS Lambda using VsCode</a>
  <a href="blogs/awsSamNetCore.html">AWS SAM .Net Core</a>
  <a href="blogs/aspnetCoreAwsLambdaServerless.html">Aspnet-core Aws-lambda Serverless</a>
  <a href="blogs/dockerFundamentals.html">Docker tutorial</a>
  <a href="blogs/enzymeTDD.html">Quick Enzyme TDD</a>
  <a href="blogs/jestTDD.html">Quick Jest TDD</a>
  <a href="blogs/jestVSmocha.html">Jest vs Mocha</a>
  <a href="blogs/keepingSecrets.html">Keeping Secrets</a>
  <a href="blogs/testQuality.html">Test Quality</a>
  <a href="blogs/pairProgramming.html">Pair Programming</a>
  <a href="blogs/migrateRepoFromTfsToGithub.html">Migrate repository from TFS to Github</a>
  <a href="blogs/awsECSDocker.html">AWS ECS and Docker Quick Guide</a>
  <a href="blogs/1-1.html">The 1-1s</a>
  <a href="blogs/em.html">The Engineering Manager</a>
  <a href="blogs/juniorMidSenior.html">Junior Mid Senior Developers</a>
  <a href="blogs/doingDevOpsRight.html">DoingDevOpsRight</a>
</div>

<br>
  <button class="openbtn" onclick="openNav()">&#9776; Browse Blogs</button>
<br>
<br>

<div class="pad">
  {{ site.time | date_to_long_string }}
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
</div>