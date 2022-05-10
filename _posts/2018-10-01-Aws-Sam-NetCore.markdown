---
layout: post
title: Aws Sam .Net Core
date: 2018-10-01
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: awsSam.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Docker,AWS ECS] # add tag
---

# Aws Sam Tutorial

## What is the AWS Serverless Application Model?

The AWS Serverless Application Model allows you to describe or define your serverless applications, including resources, in an easier way, using AWS CloudFormation syntax. In other words, AWS SAM is a CloudFormation extension optimized for serverless applications. It supports anything that CloudFormation supports. You can use YAML or JSON syntax to write your templates.
Clear enough? Maybe not. To understand it better, let’s look at a very simple example.

## Prerequisites

### Installing Docker

Docker is an open-source software container platform that allows you to build, manage and test applications, whether you're running on Linux, Mac or Windows. For more information and download instructions, see Docker.

Once you have Docker installed, SAM CLI automatically provides a customized Docker image called docker-lambda. This image is designed specifically by an AWS partner to simulate the live AWS Lambda execution environment. This environment includes installed software, libraries, security permissions, environment variables, and other features outlined at Lambda Execution Environment and Available Libraries.

Using docker-lambda, you can invoke your Lambda function locally. In this environment, your serverless applications execute and perform much as in the AWS Lambda runtime, without your having to redeploy the runtime. Their execution and performance in this environment reflect such considerations as timeouts and memory use.

#### Important

**Because this is a simulated environment, there is no guarantee that your local testing results will exactly match those in the actual AWS runtime.**

### Installing SAM CLI

SAM CLI is a tool that also allows faster, iterative development of your Lambda function code, which is explained at Test Your Serverless Applications Locally Using SAM CLI (Public Beta). To use SAM CLI, you first need to install **Docker**.
The easiest way to install SAM CLI is to use pip.

You can run SAM CLI on Linux, Mac, or Windows environments. The easiest way to install SAM CLI is to use pip.

To use pip, **you must have Python installed** and added to your system's Environment path.

```Powershell
pip install aws-sam-cli
```

Then verify that the installation succeeded.

```Powershell
sam --version
```

You should see something similar to the following:

```Powershell
SAM CLI, version 0.3.0
```

## Lets start with a Hello World

To get started with a project in SAM, you can use the sam init command provided by the SAM CLI to get a fully deployable, boilerplate serverless application in any of the supported runtimes. sam init provides a quick way for you to get started with creating a Lambda-based application and augment into a production application by using other commands in the SAM CLI.

To use sam init, navigate to a directory where where you want the serverless application to be created. Using the SAM CLI, run the following command (using the runtime of your choice. The following example uses Python for demonstration purposes.):

```Powershell
$ sam init --runtime dotnet
[+] Initializing project structure...
[SUCCESS] - Read sam-app/README.md for further instructions on how to proceed
[*] Project initialization is now complete
```

This will create a folder in the current directory titled sam-app. This folder will contain an AWS SAM template, along with your function code file and a README file that provides further guidance on how to proceed with your SAM application. The SAM template defines the AWS Resources that your application will need to run in the AWS Cloud.

The folder structure will include the following:

- A helloworld directory that includes an program.cs file that contains sample code which is a simple lambda return the ip as an api gateway response:

```csharp
...

namespace HelloWorld
{

    public class Function
    {

        private static readonly HttpClient client = new HttpClient();

        private static async Task<string> GetCallingIP()
        {
            client.DefaultRequestHeaders.Accept.Clear();
            client.DefaultRequestHeaders.Add("User-Agent", "AWS Lambda .Net Client");

            var stringTask = client.GetStringAsync("http://checkip.amazonaws.com/").ConfigureAwait(continueOnCapturedContext:false);

            var msg = await stringTask;
            return msg.Replace("\n","");
        }

        public APIGatewayProxyResponse FunctionHandler(APIGatewayProxyRequest apigProxyEvent, ILambdaContext context)
        {

            string location = GetCallingIP().Result;
            Dictionary<string, string> body = new Dictionary<string, string>
            {
                { "message", "hello world" },
                { "location", location },
            };

            return new APIGatewayProxyResponse
            {
                Body = JsonConvert.SerializeObject(body),
                StatusCode = 200,
                Headers = new Dictionary<string, string> { { "Content-Type", "application/json" } }
            };
        }
    }
}
```

- A aws-lambda-tools-defaults config for the lambda and its settings 

```json
{
  "Information": [
    "This file provides default values for the deployment wizard inside Visual Studio and the AWS Lambda commands added to the .NET Core CLI.",
    "To learn more about the Lambda commands with the .NET Core CLI execute the following command at the command line in the project root directory.",
    "dotnet lambda help",
    "All the command line options for the Lambda command can be specified in this file."
  ],
  "profile": "default",
  "region": "us-east-2",
  "configuration": "Release",
  "framework": "netcoreapp2.1",
  "function-runtime": "dotnetcore2.1",
  "function-memory-size": 256,
  "function-timeout": 30,
  "function-handler": "HelloWorld::HelloWorld.Function::FunctionHandler"
}
```


- A sample template YAML file that describes your SAM application:

```yaml

AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: >
    Sample SAM Template for sam-app

# More info about Globals: https://github.com/awslabs/serverless-application-model/blob/master/docs/globals.rst
Globals:
    Function:
        Timeout: 10


Resources:

    HelloWorldF1unction:
        Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
        Properties:
            CodeUri: src/HelloWorld/bin/Debug/netcoreapp2.1/publish
            Handler: HelloWorld::HelloWorld.Function::FunctionHandler
            Runtime: dotnetcore2.1
            Environment: # More info about Env Vars: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#environment-object
                Variables:
                    PARAM1: VALUE
            Events:
                HelloWorld1:
                    Type: Api # More info about API Event Source: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api
                    Properties:
                        Path: /hello
                        Method: get

```

I have removed or omitted the output section as its not required for this.

## Run lambda api locally

- Build and Publish the project and run lambda api through sam

```Powershell
cd $PROJECT_PATH
dotnet build
dotnet publish
sam local start-api
```

In your browser try hosted link from the out put http://localhost:3000/hello 

And voila you have a runner :+1:

## Advance concepts

### AWS CLI

- Configuring and creating your user account [more](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)

### IAM Credentials

- SAM CLI will invoke functions with your locally configured IAM credentials.

As with the AWS CLI and SDKs, SAM CLI will look for credentials in the
following order:

1. Environment Variables (``AWS_ACCESS_KEY_ID``,
   ``AWS_SECRET_ACCESS_KEY``).
2. The AWS credentials file (located at ``~/.aws/credentials`` on Linux,
   macOS, or Unix, or at ``C:\Users\USERNAME \.aws\credentials`` on
   Windows).
3. Instance profile credentials (if running on Amazon EC2 with an
   assigned instance role).

[more](https://github.com/awslabs/aws-sam-cli/blob/develop/docs/advanced_usage.rst#iam-credentials)

### Missing dependencies for .Net Core

- **The More Lightweight, DevOps-Friendly Fix**

Thanks to this thread on StackOverflow and a comment from Nate McMaster, there’s an easier way to do this that doesn’t require editing your csproj file.  Turns out that there’s an undocumented /property command line option for “dotnet publish” that lets you pass msbuild variables in.  Supply the following /property value and it causes dotnet publish to publish all the dependencies.

```powershell
dotnet publish -o .\output /property:PublishWithAspNetCoreTargetManifest=false
```

[more](https://stackoverflow.com/questions/43837638/how-to-get-net-core-projects-to-copy-nuget-references-to-build-output/43841481)