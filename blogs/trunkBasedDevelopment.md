---
layout: default
title: Trunk Based Development
subtitle:
date: March 06, 2019
author: Arvin Bhurtun
---
{% feed_meta %}
{% seo %}


# Trunk Based Development

{{ page.date | date_to_string }} {% include readTime.html %}

Every time there is talk about trunk-based development or developing in master, people have are hesitant, resistant and find the whole idea weird or that you are a "cowboy". Mainly it’s because they think I’m saying that they’re wrong. This is one of my favorite topics as it's a prerequisite for continuos delivery. It simplifies code pushes and improves the frequency of deployments. Until I tried it, I didn’t get why trunk-based development was a good thing. Or that I shouldn’t be afraid of pushing code directly to the master branch without a pull/merge request. That’s why I want to share my experience as to why you need this practice in your teams. My reasons to use trunk-based development are listed below. That said am i no means suggesting that all other ways are wrong. There might be clear business or legacy reasons why you would adopt a different approach for example feature branching.

## Trunk-Based Development

Let’s start with the [definition](http://trunkbaseddevelopment.com) of trunk-based development
> “A source-control branching model, where developers collaborate on code in a single branch called trunk [or master in Git], resist any pressure to create other **long-lived development branches** by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after.”

The definition doesn’t say you **no longer use branches.** You can continue using branches, as long as they’re short-lived branches. With trunk-based development, you reduce the scope of the change, and you get feedback from everyone more quicker. Everyone will always have the latest version of the code that’s running in production. The trunk-based development practice ends up being more a mindset change than a technical change. A developer won’t “hide” the work in progress but rather makes it visible to a broader audience sooner. You can continue working with any branching strategy, but at some point, it will become an additional process. It’s way simpler working directly in the master branch. It forces the developers to think early on about how not to break the build, instead of waiting to think about this when merging the branch. So no, trunk-based development doesn’t mean that you’ll no longer use branches. You’ll still use them but in a different manner. 

## Benefits

### Integrate Code Continuously

Pushing your code changes directly to the master branch, means you no longer have to go through the merge process (which we all know can be painful, stressful, and boring).

For example, configure your integration server to build from the master branch. As soon as changes are pushed, integrate the code right away. When the integration phase starts, it’s time to validate the code the developer is pushing compiles and that all tests unit,integration and automation pass.

It is critical to have a reliable battery of tests and [a good testing strategy](https://rollout.io/blog/testing-strategies-delivery-pipeline/). It’s not just about unit tests; you could consider a few integration tests, graphic user interface (GUI) tests, and also run a static analysis. Let’s forget about the happy route, where everything works and the change is simple and won’t break anything. Let’s focus then on the scenario where something goes wrong. The first thing that will happen is the team will get a notification that the build is failing. The intention behind that is to give everyone a chance to review what’s happening and maybe provide input that could help solve the problem. Following the [“Andon” cord practice](https://itrevolution.com/kata/), fixing the build will be the team’s highest priority. If the team can’t apply a fix in at least ten minutes, everyone should agree to roll back the change. But trunk-based development becomes more natural to adopt when you use [feature flags in your continuous integration](https://rollout.io/blog/value-feature-flags-ci-cd/) pipeline. Turn off the feature flag and let the team continue working with a stable version and a healthy build. You can address the problem more calmly later. 

### Eager and Continuous Code Review

In my opinion, code reviews are more productive by pair-programming with a peer. But the team might be too small for that. Or maybe management doesn’t like the idea of having two folks working on one thing that a single person could do. If you’re not doing code reviews with pair-programming, then the traditional way is to create pull/merge requests and assign it to a peer in the team. That person will first need some context, and usually a lot of time if it’s a significant change. When a change is too large, the person reviewing the code might ignore or miss important things. Whereas if the change is small, it’s easier to make useful recommendations. Even better if the review is happening in real time. If you push directly to the master branch frequently (as you do with trunk-based development), code review requests will increase. You might want to get help from external tools that will validate that there aren’t security issues, no one wrote a code portion twice, and that the code complies with the team standards (naming conventions, tabs vs. spaces, etc.). If something is outside the norm, you could either break the build and force the review from the team. Or you could create warnings that the developer will fix later, but before the change goes live. Feedback is crucial in every continuous integration and delivery pipeline. With trunk-based development, you’re making sure you continually get eager feedback when it’s cheaper and you can prevent further problems. Try to make code reviews small, and don’t wait until the code is ready to be promoted as you do with pull/merge requests.

### Release Application Changes Consecutively

When you’re able to integrate your code continuously with feature flags, another benefit is that you’ll be able to deploy more frequently. You can then delay the decision to release the change when you want or need to. New features will be [launched in the dark](https://rollout.io/blog/dark-launch-directors-new-best-friend/) and are ready to go live by just turning on the feature flag. You no longer need to release changes serially as long as you’ve planned it that way. That means the new features are going to be backward compatible. Even though you open the possibility of releasing application changes consecutively, I wouldn’t recommend that you accumulate too many features at the same time. The idea is that you can do deployments more frequently until they become a standard practice. And when the time comes where you need to release a bug fix, you don’t have to roll back a change or remove any code. Traditionally, rollbacks are complicated, and it requires time and effort from several people. But if you’re used to always going forward with changes, you can either release a fix in minutes or turn the feature off. It’s the simplest way to keep the path clean for any upcoming changes in the application. Simple actions like integrating to the master branch on a daily basis and wrapping changes into feature flags will allow you to release any changes in parallel. 

### Gradually Introduce New Features

After you get used to deploying incomplete changes, you start doing significant or complicated architectural changes gradually. Usually, you begin by creating the new version in a separate repository, with different infrastructure. Even if you choose a [blue/green deployment strategy](https://rollout.io/blog/blue-green-deployment/), problems always arise after switching to the latest version. Some things that used to work stop working. It doesn’t matter how careful you are when releasing significant changes, the risk of things going bad is always high. Instead, a recommended way to make large-scale architectural changes is to introduce new features into the primary system gradually. This idea comes from [Martin Fowler’s](https://twitter.com/martinfowler) post on [strangler patterns](https://www.martinfowler.com/bliki/StranglerApplication.html). In it, he says that “an alternative route is to gradually create a new system around the edges of the old, letting it grow slowly over several years until the old system is strangled.” When you need to make significant changes like going from a monolithic to a microservices architecture, the strangler pattern is a good choice. The main reason why you decide to do significant changes is that it’s getting painful to release new changes. Architecture is obsolete, or the source code is too big. Trunk-based development will help you to gradually introduce significant changes because you’re always integrating code even if it’s not complete yet.

### Not Controversial Anymore

As I said before, trunk-based development is a mindset more than a practice. It’s not easy to get it right, and it’s not for everyone. If you’re struggling with spending too much time fixing merge conflicts or recovering missing code, you might consider trunk-based development. You’ll have better delivery throughput, more application stability, and the team will be able to focus on how to deliver value more frequently. Finally, the books [The DevOps Handbook](https://www.amazon.com/DevOps-Handbook-World-Class-Reliability-Organizations/dp/1942788002/ref=sr_1_1?s=books&ie=UTF8&qid=1539389650&sr=1-1&keywords=devops+handbook) and [Continuous Delivery](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912) spend more than a few pages talking about this. [DevOps reports and case studies](https://devops-research.com/assets/capital_one_case_study.pdf) also confirm that people who practice trunk-based development increase the delivery throughput. It shouldn’t be controversial anymore.

---

Return to [Blogs](../index.md).