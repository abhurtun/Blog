---
layout: default
title: AWS ECS and Docker Quick Guide
subtitle:
date: Febuary 11, 2020
author: Arvin bhurtun
---
{% seo %}


# AWS ECS DOCKER Quick Guide

{{ page.date | date_to_string }} {% include readTime.html %}

{% include likeButton.html %}

## Docker summary

Docker Containers are like the boxed-spaces where we can build anything inside. 
On the outside there are hookups for utilities.
Docker Images are like the boxed-space blueprints.
Servers set up for Docker are like hosts set up to plug-n-play these boxed-spaces.

## Challenges with Managing Docker Containers

- Monitoring each of the Docker Containers on the different servers
- Monitoring the servers themselves
- Managing usage of space, resources, power, etc of the servers
- Directing traffic to the most appropriate Container within the most appropriate server
- Adding removing Containers if traffic levels demand it
- Updating all of the Containers if the Docker Image changes

## AWS EC2 Container Service aka "ECS"

ECS solves the previously mentioned challenges. In a simple terms: "ECS manages and deploys Docker Containers."

## Clusters and the ECS Container Agent

A Cluster is a group of EC2 instances, that each have an ECS Container Agent on them configured to point the same Cluster.

- The EC2 Instances -> hosts.
- The Cluster -> Group of hosts.
- The ECS Container Agent is on each hosts, that reports back on the status of the host itself and it's containers.

## Simple Setup of a cluster

1. Create a Cluster using AWS CLI

    ```powershell
    aws ecs create-cluster --cluster-name "my-cluster"
    ```

2. Create the IAM Role for the EC2 Instances to be used in the Cluster

    EC2 instances that hook up with ECS need an IAM role with the AmazonEC2ContainerServiceforEC2Role policy. This is actually a managed policy, meaning that it's pre-made. So all that's need to create this role is to:

    - Create a new IAM role with the type: Amazon EC2 Role for EC2 Container Service

    - Select the AmazonEC2ContainerServiceforEC2Role policy

3. Set up EC2 instances with the ECS Container Agent

    The best way to create an instance that's ready to hook up with ECS is to just use the AMI "ECS Optimized AMI"

4. Point the ECS Container Agent on the instances to the Cluster

    If we're using the ECS Optimized AMI add to config file /etc/ecs/ecs.config

    ```
    ECS_CLUSTER=YOURCLUSTERNAME  
    ```

    You can do this using a user data script. The script can either write to the ECS_CLUSTER variable itself or we can keep our config file in a secure S3 bucket and pull it in.

5. Launch the instances!

    The instances will automatically "join" the Cluster

# Task Definitions

A Task Definition is a specification of exactly what's needed to set up our container(s) in our Container Instances. 

For example, Ransom "Task Definition" might consist of:

- Docker Image for Marvel app

- Docker Image for DC app

- the cpu, memory, port mappings, entry points, etc for each to-be-made Container

You can use aws cli and have a template for your task definition eg.[The AWS Task Definition Template](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-task-definition.html#task-definition-template)

**Important properties in the template:**

- Properties of **containerDefinitions** like CPU and Memory ,You'll need to figure out what each of your container needs and uses.
- **essential** property on a containerDefinition means that if that that container goes down, they all do.
- **entrypoint** and **command** just overwrite whatever you have in the image. **You don't have to re-define.**
- **links** specify how containers can communicate with each other. It's like using the --link option in docker run.

# Apply Task Definitions

## Running a Task

The process of running invloves the Cluster taking the "Task Definition", Coordinating with all ECS Container Agents and find Server is the best fit.
When running a Task, we can specify to run more than 1 Task. 

This is the equivalent of saying:
"Given my Ransom Task Definition, make 3 Tasks from it." which would result in 3 pairs of apps.

There's 5 main strategies we get to select from:

1. AZ Balanced Spread - Spreads Tasks evenly across AZ's. Within an AZ, it spreads Tasks evenly among Instances.

2. AZ Balanced Binpack - Spreads Tasks evenly across AZ's. Within an AZ, it tries to use the least amount of Instances. How? By prioritizing Instances with the least amount of available CPU or memory.

3. Binpack - Places tasks on instances with the least amount of CPU or Memory. Doesn't care about AZ spread.

4. One Per Host - One per Instance.

5. Custom - Allows the user to customize the placement from a set of options. This allows us base spread on something like OS type or AMI ID as well. The docs are basically non-existent on how they work though.

[Amazon ECS Task Placement Strategies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html)

## Creating a Service

Running a Task is a one time type thing. To remember it, think "one and done" because it's "run and done."

Creating a Service tells our Cluster to go beyond just running Tasks - it manages them. We create a Service and hand it a Task Definition. It takes the Task Definition and does a number of things for us. Specifically:

1. Sets up our Tasks from our Task Definitions on the best suited Container Instances (same as running a Task).

2. Monitors our Tasks and reports back metrics

3. Keeps the number of Tasks we specify always up and running

4. Updates our Tasks by handing them an updated Task Definition

5. Optionally scales out/in our Tasks based on customer demand (traffic)

6. Distributes our customer demand evenly to all Tasks via Load Balancer (if we hook one up)

## Application Load Balancers

Application Load Balancers are needed to direct traffic to Containers. They allow for a variety of powerful concepts like name-spacing sets of containers as "Target Groups." This allows us to direct traffic to different sets based on rules like the request Protocol or Path.

---

Return to [Blogs](../index.md).