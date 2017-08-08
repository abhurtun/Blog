---
layout: default
title: Migrate repository from TFS to Github
subtitle:
date: August 8, 2017
author: Arvin bhurtun
---

# Migrate repository from TFS to Github

{{ page.date | date_to_string }} {% include readTime.html content=post.content %}read

{% include likeButton.html %}

## What you'll need before you start
* Name of old TFS repository
* Version number within the old TFS repository you want to migrate history from (important with big, old projects)
* Git-TF (see installation instructions below)
* New Github repository

### Install Git-TF
If you don't already have Git-TF, you can either use [Chocolatey](https://chocolatey.org/) with `cinst Git-TF`, or download it manually from the [Git-TF project page](https://gittf.codeplex.com/).

### Create a new Github repository
Log into Github and create a new repository with the name of project. This may be different from the old TFS name as some repository naming conventions have changed. NB. You may need someone else to do this for you if you don't have permission.

## Clone the TFS repository as a Git repository
Within your git workspace (typically, `C:\Git`), type the following command (and when promted use the administrator's credentials):

```sh
git tf clone --deep http://my-tfs:8080/tfs/Tfs {src-repo} .
```

NB. {src-repo} is the TFS repo path, but with the `/` changed to `\`. If you fail to do this, you may get a `git-tf: A server path must be absolute.`

But, if the repository is too big (too many commits), then you may also do:

```sh
git tf clone --shallow --version={n} http://my-tfs:8080/tfs/Tfs  {src-repo} .
git tf pull --rebase --deep
```
E.g. For SAPI, the shallow command looked like:

```sh
git tf clone --version=69919 --shallow http://my-tfs:8080/tfs/Tfs  $\SAPI\Main .
git tf pull --rebase --deep
```
NB. If you get an error like `Unable to find a required JAR: C:\ProgramData\chocolatey\lib\Git-TF\Tools\git-tf-2.0.3.20131219/lib/com.microsoft.gittf.client.clc-*.jar does not exist`, follow the instructions at http://stackoverflow.com/questions/33915987/git-tf-unable-to-find-required-jar

## Prepare to 'Gitify' and 'NuGetify' the project
First, copy over the following Git files from the FMP project into the new Git project folder:

`.gitignore`
`.gitattributes`

Then, for the solution folder, copy over into a new `.nuget` folder from the FMP project:

`.nuget\nuget.config`

## Clean the solution
Remove `*.vs{aa}cc` files and the `packages` folder.

Open the solution in Visual Studio:
* Ensure it doesn't have any links to TFS; if it does, remove them
* Force a save by creating a new folder, saving the solution and then deleting the folder and re-saving the solution

## Incorporating NuGet into the solution
* Add the `.nuget` folder into the solution
* Build the solution

## Clean the Git repository
Run the following script to remove the `packages` folder from the repository:

```sh
git filter-branch --index-filter "git rm -r --cached --ignore-unmatch packages/" --prune-empty --tag-name-filter cat -- --all
```

## Push to Github
Set the Git remote to that of the Github repository url, and then push to Github by running the following:

```sh
git remote add origin {git-repo-link}
git push origin master --force
```

## Update the TeamCity build to use Git, rather than TFS
1. Go to the TeamCity project and choose __Edit Project Settings__
2. Then choose __VCS Roots__
3. For each item in the list perform the following:
  1. Change __Type of VCS__ to __Git__
  2. Change __Fetch URL__ to that of the Github repository (using the format git@github.com:findmypast/{repository}.git)
  3. Change __Authentication method__ to __Uploaded Key__
  4. Change __Uploaded Key__ to __teamcity-fmp__
  5. (Click Advanced Settings if necessary)
  6. Tick __Convert line-endings to CRLF__
  7. Hit the __Test connection__ button
  8. Hit the __Save__ button

## Update TeamCity to restore NuGet
1. Within the TeamCity project choose __Edit Project Settings__
2. Then choose __Build Steps__

### Add build step to restore NuGet
3. Click __Add Build Step__
4. Choose __Runner type__ of __NuGet Installer__
5. Click __Show advanced options__
6. Set __Step name__ to that of *Restore NuGet packages*
7. Set __Path To Solution File__ by clicking the tree dropdown to the right and selecting it
8. Set __Package Sources__ to the urls contained within `.nuget\nuget.config`
9. Click __Save__

10. Hit __Reorder build steps__ and move the newly created step to the top of the list and click __Apply__
