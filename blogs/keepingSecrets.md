---
layout: default
title: Best Practices For Keeping Secrets Out of Source Control
subtitle:
date: January 31, 2018
author: Arvin Bhurtun
---
{% seo %}

# Best Practices For Keeping Secrets Out of Source Control

{{ page.date | date_to_string }} {% include readTime.html %}

{% include likeButton.html %}

## How to Keep API Keys and Secrets Out of GitHub in .NET Core

In 2015, a bug in the GitHub extension that shipped by default with Visual Studio 2015 [leaked my source code to a public GitHub repository instead of a private one](https://www.humankode.com/security/how-a-bug-in-visual-studio-2015-exposed-my-source-code-on-github-and-cost-me-6500-in-a-few-hours "How a bug in Visual Studio 2015 exposed my source code on GitHub and cost me $6,500 in a few hours").

Minutes later, bots scanning GitHub repositories for API keys and secret information grabbed my API key and started launching numerous EC2 instances. These EC2 instances are typically used for GitHub mining. Hours later, my Amazon AWS bill stood at $6,500.

This, believe it or not, is quite a common occurrence. It's so common that Amazon has their own bots that scan GitHub for API keys and will now send you an email if they detect that your key has been exposed.

Here's a guide along with some best practices to follow in .NET Core to keep private information out of Source Control.

### If You're Checking Keys Into Private Repos, You're Doing it Wrong

I committed a deadly sin by checking private keys into a private repository. All it took was a simple bug to expose my sensitive information. Developers expose API key and private information all the time. Mostly, because they're not aware of the consequences. I wasn't.

I was working on a private project and thought that checking my API keys into a private repo was perfectly safe and secure. And boy was I wrong.
If you're committing API keys, passwords or sensitive information into source control, even if it is a private repo, you're doing it wrong.

### Why Passwords and API Keys Should Never Be Checked Into Source Control

Version control systems are designed to keep a history of all commits. Once you commit to a repository, it is very hard or impossible to delete that commit. Even if this information was pushed to a private repository in your company and you manage to completely delete all traces of this information in the repo, you still wouldn't have any way of knowing how many people pulled these changes.  

Several people on your team who should not have access to this information could now have access to it. There's no way of knowing who would use the information at some point in the future.  

If information has been pushed to a public repository the information is already out in the wild, and you have to assume the worst.  
Search engines might have indexed it. Bots and people would have downloaded your code already, especially if there are passwords or API keys in there. It only takes seconds for bots to detect API keys that have been pushed to GitHub.  

Database credentials could be used to gain unauthorized access to systems.  

API keys could be used to spawn up cloud resources, which in turn could have a significant financial impact. API keys could also be used to access sensitive information stored in the cloud.  
Many companies now use the cloud as their primary mode of storing data, and an API key would allow easy access to all this information. A company's IP could easily land in the wrong hands, or worse even, data could simply be leaked online.  

Exposing something as simple as an API key could have a devastating impact.  

Avoid committing secret information to source control at all costs. The impact would likely be far-reaching and have a significant financial impact.  

From an operational point of view, let's look at how a likely scenario would play out if secrets were leaked in a corporate environment.  

API keys would have to be revoked and regenerated. Then, the new API keys would have to be re-implemented across all affected applications. As these changes would need to be made in a production environment the DevOps team will require involvement.  

Database passwords would have to be recreated, and the new credentials would have to be implemented across all affected applications. In a corporate environment, the impact of this could be significant as there could not only be a large number of affected applications, but there could be several legacy applications. It will most likely require the involvement of a large number of developers, and in the case of recreating database credentials, the DBA team will need to get involved.  

Changes will have to be tested. This will require developers from all affected teams to get involved. QA teams and product owners will require their involvement to ensure all affected applications are tested and is working as expected.  

In an enterprise environment, such a process could involve multiple teams and take several days to complete.  

Finally, it's very likely that applications will experience downtime. As a result, customers will be affected.  

It's highly likely that a developer leaking keys to a public repository could lose their job in addition to suffering reputational damage.

Don't do it. Never commit sensitive information to source control. Never. Ever. Period.

### How To Keep Configuration Settings Out of Source Control In .NET Core

Working with and storing configuration values in .NET Core has become a lot more extensible and easier than in previous .NET versions. If you've ever had to create custom configuration settings in the web.config of old, you would most certainly agree that implementing configuration using json in .NET Core is not only dead easy by comparison, but an absolute joy to work with.

Configuration in the .NET Core world has now become a huge topic in itself, and there are several ways of storing and using configuration values.  
When it comes to storing configuration values and keeping them out of source control, there are currently three ways to achieve this, of which

When it comes to storing configuration values and keeping them out of source control, there are currently three ways to achieve this, of which only one should be considered a best practice method in my opinion.  

I'll quickly cover the first two methods along with the pros and cons of each method before delving into the preferred third method into more depth.

### Using the Secrets Manager to Store App Secrets in .NET Core

The Secrets Manager is a new tool that can be used in .NET Core to store user secrets. Secrets are placed in a .json configuration file, which is placed in the user's profile relevant profile directory in Windows, Linux or Mac. Because the file is placed in the user's profile directory, the file will always be excluded from source control.  

The basic premise is that you set configuration values using the same keys as in your configuration files so that you override these values in your development environment.  

The tool is a development only tool and doesn't work in production.  

To install it, add the following line to your .csproj file

`YourProject.csproj`

    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.Extensions.SecretManager.Tools" Version="1.0.0-msbuild3-final" />
    </ItemGroup>

Then, from your console in the project for which you would like to set a secret in Visual Studio, you can set a secret like this

    dotnet user-secrets set connectionStrings:humanKode Server=localhost;Database=humankode;Uid=;Pwd=;

Then, in your startup.cs you configure the secret manager

`startup.cs`

    public Startup(IHostingEnvironment env)
    {
        var builder = new ConfigurationBuilder();

        if (env.IsDevelopment())
        {
            builder.AddUserSecrets<Startup>();
        }

        Configuration = builder.Build();
    }

And finally, to read values you do it the same as you would have read values from .json configuration files

`startup.cs`

    public class Startup
    {
        string _connectionString = null;
        public Startup(IHostingEnvironment env)
        {
            //....
        }

        public IConfigurationRoot Configuration { get; }

        public void ConfigureServices(IServiceCollection services)
        {
            _connectionString = Configuration["ConnectionStrings:HumanKode"];
        }
    }

While this method is relatively easy to use, it requires the installation of an additional tool along with the knowledge on how to use it. The barrier to entry is therefore slightly higher. When it comes to implementing a strategy for keeping secrets out of source control, it is important to implement a unified strategy on a team. It's entirely possible that this method can work quite well on teams where everyone subscribes to this methodology.  

I don't see this as a bad way to do things. It's an additional tool that must be used when there's an easier way to ensure that configuration secrets are not checked into source control using .NET core.

### Using Azure Key Vault to Store App Secrets in .NET Core

ASP.NET Core now has support for storing your app secrets in Azure Key Vault.  

It's really quick and simple to do. The process involves setting up an Azure Key Vault and creating your secrets. Then, you create a configuration file to store your Azure App Id and Secret, and add a nuget package for Azure Key Vault support.  
Finally, you simply add a few lines to your startup.cs to add Key Vault support.  

Azure Key Vault values simply chained to the configuration pipeline, meaning they overwrite configuration values with a similar key that you might have created earlier in your configuration files.  

You still need to exclude your Azure configuration file from source control, but I think it's a good way to manage secrets as you only need to ever keep track of one configuration file.  

I wrote a detailed blog post and video tutorial here : [How to Store Secrets in Azure Key Vault Using .NET Core](https://www.humankode.com/asp-net-core/how-to-store-secrets-in-azure-key-vault-using-net-core "View Post")  

### Using Environment Variables along with Configuration Files With an Ignore File in .NET Core

The third option is also the quickest and easiest to implement. It requires no additional tooling or services.  

It works by using the existing configuration features in .NET Core. To use this method, it's important to understand three very simple concepts. By combining them, you can use a fool-proof, easy to use method to ensure that your secrets are never checked into source control.

#### Understanding Environment Variables

.NET Core has built in functionality to determine the environment that you are running in. If you're developing a .NET core application in Visual Studio, the default environment is automatically set to Development through the variable name ASPNETCORE_ENVIRONMENT. If you deploy to staging or production you can set these values to Staging and Production respectively. If the ASPNETCORE_ENVIRONMENT variable is not set, it defaults to Production.

#### Setting Environment Variables in Visual Studio</div>

Specifying Environment Variables at Runtime

    dotnet run --environment "Production"

#### Understanding .NET Core Configuration: Chaining and Environment Aware Configuration

.NET Core comes with a very extensible configuration API which allows you to load any .json configuration file with minimal effort. A key feature is the ability to chain configuration files together. You could easily split configuration files and then chain them together when you load them in startup.cs. For instance, you could have appsettings.json and mailsettings.json, and when they're chained together via startup.cs all values are read out of the same scope.   

Another key concept is environment aware configuration. For instance, you can load appsettings.json and appsettings.{env.EnvironmentName}.json. By making both configuration files optional, and ensuring that appsettings.{env.EnvironmentName}.json is chained after appsettings.json, if both files are loaded, then only the last one's configuration values will be used.

Chaining configuration files together

```csharp
    public Startup(IHostingEnvironment env)
    {
         var builder = new ConfigurationBuilder()
    	  .SetBasePath(env.ContentRootPath)
    	  .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
    	  .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);

         Configuration = builder.Build();
    }
```

#### Understanding Git's .gitignore

Git provides a very easy way to exclude files from being checked into Git. Subversion and TFS also have ways of ignoring files, so the same principle can be applied if you use different version control software.

`.gitignore`

    # ignore appsettings configuration files
    **/appsettings.development.json
    **/appsettings.staging.json
    **/appsettings.production.json

#### Tying it All Together by Combining Environment Aware Configuration With .gitignore 

By tying all three concepts together, we can use the following simple but effective solution to keep sensitive configuration data out of Git.

1. Add an appsettings.development.json file to your project. Use this file for storing all your configuration values
2. Use appsettings.json only as an example template and never to store any settings. This file will be checked into source control and will be used by developers to setup their own appsettings.{env.EnvironmentName}.json file
3. Add a .gitignore rule to ignore appsettings.{env.EnvironmentName}.json

`appsettings.json`

    /*
      WARNING - This file will be checked into source control. Do not change this file.
      Use this as an example file only.
      Use {env.EnvironmentName}.json as your configuration file as it will not be checked into source control.
      {env.EnvironmentName} values : development, staging, production
    */
    {
      "appSettings": {
        "cdnBaseUrl": "https://d15r7eb41fg21z.cloudfront.net",
        "connectionStrings": {
          "humanKode": "Server=localhost;Database=database;Uid=username;Pwd=db_password;"
        },
        "oAuthConfiguration": {
          "providers": [
            {
              "name": "Google",
              "clientId": "clientId",
              "clientSecret": "clientSecret"
            },
            {
              "name": "Github",
              "clientId": "clientId",
              "clientSecret": "clientSecret"
            }
          ]
        },
        "mailSettings": {
          "fromEmail": "email1",
          "siteAdminEmails": "email1,email2",
          "smtpSettings": {
            "host": "email-smtp.us-east-1.amazonaws.com",
            "username": "username",
            "password": "amazon-aws-api-secret",
            "port": 25,
            "ssl": true
          }
        }
      }
    }

`startup.cs`

    public Startup(IHostingEnvironment env)
    {
        var builder = new ConfigurationBuilder()
            .SetBasePath(env.ContentRootPath)
            .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
            .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, reloadOnChange: true)
            .AddEnvironmentVariables();

        Configuration = builder.Build();
    }

`.gitignore`

    # ignore appsettings
    **/appsettings.development.json
    **/appsettings.staging.json
    **/appsettings.production.json

    # ignore connectionstrings
    **/connectionstrings.development.json
    **/connectionstrings.staging.json
    **/connectionstrings.production.json

    # ignore mailsettings
    **/mailsettings.development.json
    **/mailsettings.staging.json
    **/mailsettings.production.json

### Best Practices

1. Never commit any secrets to source control, even if it's a private repository.
2. Use multiple configuration files instead of one big one. For instance, keep connection strings in connectionstrings.development.json, general settings in appsettings.development.json, mail settings in mailsettings.development.json and so forth.
3. Never hard-code configuration values in code.
4. Document the process of keeping secrets out of source control, and make sure everyone on your team is on board with the process. All new developers must use the same process. It only takes a single mistake to expose sensitive information.
5. Always make sure that ignore rules exist for new configuration files.
6. Double check commits in the git staging area before committing.

### Related Posts

* [How to Store Secrets in Azure Key Vault Using .NET Core](https://www.humankode.com/asp-net-core/how-to-store-secrets-in-azure-key-vault-using-net-core)

### Resources

* [Best practices for private config data and connection strings in configuration in ASP.NET and Azure](https://www.hanselman.com/blog/BestPracticesForPrivateConfigDataAndConnectionStringsInConfigurationInASPNETAndAzure.aspx) - By Scott Hanselman

---

Return to [Blogs](../index.md).