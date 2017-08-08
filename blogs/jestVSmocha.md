---
layout: default
title: Jest Vs Mocha
subtitle:
date: July 25, 2017
author: Arvin bhurtun
---

# React Testing - Jest or Mocha? 

{{ page.date | date_to_string }} read

{% include likeButton.html %}

Both [Jest](https://facebook.github.io/jest) and [Mocha](https://mochajs.org) seem to be popular within the React community. There are tons of folks using Jest, though others seem to prefer Mocha (for example, the [Enzyme](http://airbnb.io/enzyme/) docs and examples use Mocha). So which one should you choose, and does it even matter?  

I recently started a project using [TypeScript](https://www.typescriptlang.org), and we put some effort into researching which testing framework to use. In this post, I’ll discuss what we learned and highlight a few scenarios that may lend themselves to one over the other.

## Jest

Jest is a testing framework authored by Facebook.

I wrote a blog post for it not too long ago [JestTDD](https://abhurtun.github.io/Blog/blogs/jestTDD.html)

> Although Jest may be considered React-specific test runner, in fact it is a universal testing platform, with the ability to adapt to any JavaScript library or framework. You can use Jest to test any JavaScript code. Facebook have poured a ton of work into Jest over the past year, adding new features and improvements and the revamping process started with the release of [Version 15](https://facebook.github.io/jest/blog/2016/09/01/jest-15.html) late last year.

### Strengths of Jest

The biggest advantage of using Jest is that it works out of the box with minimal setup or configuration. Much of this is because it comes with an assertion library and mocking support. The tests are written in BDD style, similar to any other modern testing library. You can literally just put your tests inside of a directory called `__tests__` or name them with a `.spec.js` or `.test.js` extension, then run `jest` and it works. That is pretty sweet.

Jest also supports [snapshot testing](https://facebook.github.io/jest/docs/snapshot-testing.html#content), which can be really handy for preventing accidental UI regressions when doing React development. These tests record snapshots of rendered component structure and compare them to future renderings. When they don’t match, your test fails, indicating that something has changed. You can easily tell Jest to update the snapshot if this change is expected (e.g. for a newly added feature).

### Weaknesses of Jest

Jest’s biggest weaknesses stem from being newer and less widely used among JavaScript developers.

It has less tooling and library support available compared to more mature libraries (like Mocha). Sometimes this type of tooling can be really handy, like the ability to run and debug your tests in an IDE but now support has been added now to my favorite [VsCode](https://code.visualstudio.com/).

## Mocha

Like Jest, Mocha is also a JavaScript testing framework. It’s an older, more mature, and less opinionated solution. It’s also more widely used—largely because of its age.

### Strengths of Mocha

Mocha’s greatest strength is its flexibility. It doesn’t come with an assertion library or mocking framework. Instead, you choose to use whatever helper libraries/frameworks that you want. [This SO post](http://stackoverflow.com/questions/10472152/standalone-assertion-libraries) discusses some of the popular JavaScript assertion libraries. One popular choice is to use Chai for test assertions and [Sinon](http://sinonjs.org/) for mocking.

Because of its maturity and widespread adoption, there is a lot of tooling built up around Mocha.

Lastly, the Mocha community is large, and there is a lot of support available in the form of videos, blog posts, and libraries.

### Weaknesses of Mocha

Mocha’s main weakness is that it requires more configuration.

You have to explicitly choose and install an assertion library, mocking framework, etc. If you value this flexibility, that can be great, but if you don’t, it can be frustrating.

You can use snapshot testing with Mocha, but it’s not as easy to integrate. Like most things with Mocha, there is a library called [chai-jest-snapshot](https://github.com/suchipi/chai-jest-snapshot) that helps integrate this functionality However, it’s yet another thing to set up.

## Recommendation

So which testing framework should you choose? I don’t think there’s a bad choice since you can make either work with some amount of effort. However, given the recent investments that Facebook has been making and the general positive response from the React community, I would recommend giving Jest a shot, unless:

*   You have identified parts of your tool chain that don’t support Jest
*   You have a large interest in future flexibility–being able to swap out assertion, mocking, other test libraries, etc.
*   You place a lot of value in having a large archive of support (e.g., blog posts, videos, libraries, etc.). It seems like Mocha has been used for everything under the sun, and I’m always able to find a blog post explaining how to use Mocha with Library X or some new JavaScript feature, such as async/await.

In short whether you choose Mocha or Jest, either will be just fine. :+1:
**Just make sure you follow your software principles and TDD all the way.**