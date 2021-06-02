---
layout: default
title: Continuos Delivery
subtitle:
date: June 02, 2021
author: Arvin Bhurtun
---

{% seo %}

## Concepts

Continuous integration is a coding philosophy and set of practices that drive development teams to implement small changes and check in code to version control repositories frequently. The goal of CI is to establish a consistent and automated way to build, package, and test applications.  

Continuous delivery picks up where continuous integration ends. CD automates the delivery of applications to selected infrastructure environments. Most teams work with multiple environments other than the production, such as development and testing environments, and CD ensures there is an automated way to push code changes to them.

The holy grail 😊, Continuous deployment goes one step further than continuous delivery. With this practice, every change that passes all stages of your production pipeline is released to your customers. There's no human intervention, and only a failed test will prevent a new change to be deployed to production.

Two biggest impediments to continuous delivery: enterprise architecture, and organizational culture. One should not underestimate the amount of will power and thrust required to get the changes through.

## What is Continuous Delivery?

Continuous Delivery is the ability to get changes of all types—including new features, configuration changes, bug fixes and experiments—into production, or into the hands of users, safely and quickly in a sustainable way.

Our goal is to make deployments—whether of a large-scale distributed system, a complex production environment, an embedded system, or an app—predictable, routine affairs that can be performed on demand.

We achieve all this by ensuring our code is always in a deployable state, even in the face of teams of thousands of developers making changes on a daily basis. We thus completely eliminate the integration, testing and hardening phases that traditionally followed “dev complete”, as well as code freezes.

## Why continuous delivery?

Wrong assumption :-1: frequent deployment, leads to lower levels of stability and reliability in our systems. In fact, peer-reviewed research shows that this is not the case—high performance teams consistently deliver services faster and more reliably than their low performing competition. This is true even in highly regulated environments such as financial services and government. This capability provides an incredible competitive advantage for organizations that are willing to invest the effort to pursue it.

Benefits :fire:

- **Low risk releases.** The primary goal of continuous delivery is to make software deployments painless, low-risk events that can be performed at any time, on demand and not a circus. By applying patterns such as blue-green deployments it is relatively straightforward to achieve zero-downtime deployments that are undetectable to users.

- **Faster time to market.** It’s not uncommon for the integration and test/fix phase of the traditional phased software delivery lifecycle to consume weeks or even months. When teams work together to automate the build and deployment, environment provisioning, and regression testing processes, developers can incorporate integration and regression testing into their daily work and completely remove these phases. We also avoid the large amounts of re-work that plague the phased approach.

- **Higher quality.** When developers have automated tools that discover regressions within minutes, teams are freed to focus their effort on user research and higher level testing activities such as exploratory testing, usability testing, and performance and security testing. By building a deployment pipeline, these activities can be performed continuously throughout the delivery process, ensuring quality is built in to products and services from the beginning.

- **Lower costs.** Any successful software product or service will evolve significantly over the course of its lifetime. By investing in build, test, deployment and environment automation, we substantially reduce the cost of making and delivering incremental changes to software by eliminating many of the fixed costs associated with the release process.

- **Better products.** Continuous delivery makes it economic to work in small batches. This means we can get feedback from users throughout the delivery lifecycle based on working software. Techniques such as A/B testing enable us to take a hypothesis-driven approach to product development whereby we can test ideas with users before building out whole features. This means we can avoid the 2/3 of features we build that deliver zero or negative value to our businesses.

- **Happier teams.** Peer-reviewed research has shown continuous delivery makes releases less painful and reduces team burnout. Furthermore, when we release more frequently, software delivery teams can engage more actively with users, learn which ideas work and which don’t, and see first-hand the outcomes of the work they have done. By removing the low-value painful activities associated with software delivery, we can focus on what we care about most—continuously delighting our users.

## Summary

There are five principles at the heart of continuous delivery:

- Build quality in
- Work in small batches
- Computers perform repetitive tasks, people solve problems
- Relentlessly pursue continuous improvement
- Everyone is responsible

## OKRs

|Pillars|Goals (Lag Measures)|<p>Key Result (Lead Measures)</p><p></p>|
| :- | :- | :- |
|<p>Culture</p><p></p>|Frequent releases & Ownership|<p>- Lean release process limit manual steps</p><p>- Review branching strategy</p><p>- Feature toggling/Experimentation</p><p></p>|
||Knowledge sharing|<p>- Infrastructure as code with Kubernetes and Docker</p><p>- Communication between teams</p>|
|<p>Continuous Improvement</p><p></p>|Slice of cake|<p>- Small user stories</p><p>- Avoid spilling stories over sprints</p><p></p>|
||Scalable Architecture|<p>- Spike early </p><p>- POCs Clear Outcomes</p><p>- Define MVP</p><p>- Deliver in iterations</p>|
|Quality|Fail Fast|<p>- Increase and monitor test coverage</p><p>- Committing code frequently</p><p>- Production-like environments with docker</p>|
||Automated QA|<p>- Reduce manual testing</p><p>- Feedback loop with development</p><p>- Automation test written by the whole team</p>|
|<p>Customer Value</p><p></p>|<p>Fully automated deployments</p><p></p>|<p>- Review data migrations</p><p>- “One-click” promotion to production</p>|
||Measure success|- Define measurable metrics|

---

Return to [Blogs](../index.md).