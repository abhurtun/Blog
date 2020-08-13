---
layout: default
title: Managing Cross-team Dependencies
subtitle:
date: Jan 30, 2019
author: Arvin bhurtun
---
{% seo %}


# Managing Cross-team Dependencies

{{ page.date | date_to_string }} {% include readTime.html %}

{% include likeButton.html %}

## Intro

Cross-team dependencies can be painful and cause friction in an organization. Unmanaged it will result into missed deadlines, non-stop meetings and chaotic context switching.

We have to be pragmatic. Sometimes teams will be blocked because their work is low priority and more strategic initiatives cannot be interrupted. If there is no interaction between teams, we will have a fragmented user experience.

The challenge is finding the right balance between collaborating and delivery. It’s risky to sit at either extreme.

## Eliminating Dependencies Organization Level

The best way to deal with the dependencies is not have them. Our default approach should always be to eliminate the dependency altogether

There are few organization patterns we can use:

* Slice and Scatter
* Slice and Merge

Slice and Scatter approach is to break the dependency down into technical components and distribute to the teams that depend on them.

> For example the “big project” has dependency on a system own by a team, so that part of the journey natural sits with that team

Slice and Merge approach is identify the dependency that affects multiple teams, change the teams and merge them into a new team that had own the dependency.

A common example of Slice and Merge is moving from activity-oriented teams (frontend, backend, DBA, etc) to vertically-sliced capability teams.

> For example “Legacy Monolith Application” decommissioning affects all teams but not owned by any delivery teams. Have a new team or working group which will work on that decommissioning and remove the dependency for other teams.

## Minimize dependencies Team level

### Inner Sourcing

This is is based on the open source development model. Team A needs Team B to make changes, but Team B has other priorities and Team A is blocked, Team A can make changes to Team B’s code and submit a pull request.

This is quite effective practice but has one drawback whereby the team accepting the pull request and  having to dedicate time to support and deal with the pull request.

### Full-stack feature teams

An easy way of removing dependencies is for “the team” to be made up of people with all the skills needed to complete the work needed. We often call these “full-stack” or “feature teams”. Teams that are building a product feature end-to-end reduce dependencies on external teams and individuals. They move quickly, add more value, and they reduce dependencies. If you can’t quite get to long-lived cross-functional feature teams, one very effective way to resolve dependencies is to have a person from the team on which you are most dependent “injected” into your team as a resource. This is often true for infrastructure, design and support teams but can be used in teams where one team is regularly dependent on another.
Rotation of team members

Regular rotation of people between teams so that individuals have a wider knowledge of the ecosystem beyond what they are currently working on. When a cross-team dependency occurs, the knowledge in the teams and improved personal working relationship due to rotating will reduce the impact of dependencies.

### Temporary Pairs

A person from Team A and a person from Team B can temporarily team up to deal with a dependency.

For example doing something innovative that cuts across multiple teams we can form a short/mid-term discovery team composed of multiple people from each team.

In this scenario we be optimizing for speed of innovation and have a single team which can move fast.

This approach also lends itself well to micro teams pattern, where overall teams are larger, and within them people continuously form temporary sub-teams based on the available work.

### Peer-to-peer collaboration between teams

While time-consuming, this is the best way to resolve dependencies. Product managers should have regular meetings. The structure of this meeting should be to talk about all the dependencies that are in progress, confirm that the dependencies they are working on are still priority, prioritize or re-prioritize new dependencies, and check how dependencies are adhering to the organization goals. This will also be a good time for every manager in the program to understand the amount of work the other teams have and then help each other out with resources or scope changes.

### Anticipating Cross-team Dependencies

It’s always sensible to anticipate ahead of time dependencies that are likely to arise.
If we think that certain dependencies may arise, we can put in place lightweight controls that enable us to better respond to them.

To help us anticipate likely dependencies, we can use visualization techniques such as EventStorming, value stream mapping, and portfolio kanban boards.

### A visual representation of the product feature backlog

The dependency board is a great way to visualize cross-team dependencies.  It allows teams to commit to working together to complete working software.  By setting a scheduled meeting to review the dependency board, we make sure that all teams are aware of any cross-team dependencies and we don’t have any cross-team dependency surprises later on in the sprint.

This technique requires all the product managers to provide a visual representation of their particular product feature backlog. Once that is done, the teams should only commit to in the following, in order of priority:

* Dependencies related to high priority features from an organizational standpoint;
* Features near completion;
* Features built on capabilities already present.

For special situations when something needs to be done outside these three cases, a special team of experts should be formed and tasked with completing it.

# Conclusion

Although dependencies may be difficult to manage they are part of agile organizations with cross-functional teams. If cross-team dependencies  are well managed, it’s an indication that there are less team silos and more collaboration. Flagging dependencies early will help to  highlight the effects on delivery and help prioritize business goals.

---

Return to [Blogs](../index.md).