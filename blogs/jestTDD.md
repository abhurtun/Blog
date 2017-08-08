---
layout: default
title: Jest REACT Enzyme TDD
subtitle:
date: July 24, 2017
author: Arvin bhurtun
---

# React + enzyme + Jest TDD

{{ page.date | date_to_string }} {% include readTime.html content=post.content %}read

{% include likeButton.html %}

### Test Driven Development in an insane JS world

_With React becoming more and more popular with frontend, we will take a look at Jest using TDD approach._

**You can find the source code for this [tutorial on Github](https://github.com/abhurtun/JestDemo)**

So, we’ll go through all the necessary steps to implement Jest and get you started with writing tests for React components, using ES2015 syntax (but of course) using the awesome Facebook’s testing framework [Jest](https://facebook.github.io/jest/). While we’re at it, we’ll set up a constant test runner for **TDD**:

### What we’ll cover:

*   Set up a simple test 
*   Setup using React and Jest
*   Cover the basics of the Jest library
*   Have a working TDD test runner

### What is Jest, first and foremost?

_“Jest is a JavaScript Testing framework which works out of the box, provides instant feedback and promotes zero-configuration experience.Capture snapshots of React trees or other serializable values to simplify testing and to analyze how state changes over time.Jest parallelizes test runs across workers to maximize performance. Console messages are buffered and printed together with test results. Sandboxed test files and automatic global state resets for every test so no two tests conflict with each other.”_

## Getting Started

Let’s start a project from scratch by downloading and installing the latest version of [node](https://nodejs.org/en/download/).

The structure for this project will be the usual application structure: project in a folder of your choice, our code will live in the `src` folder and our tests will live under the `test` folder. Setting up our structure, then:

`mkdir src test`

## Testing Dependencies

For now, grab Jest:

`npm install --save-dev jest`


## Setting up the testing framework

Once we have tests and everything wired up, we could manually run the scripts to run Jest with all the necessary parameters, but we don’t have to. We can make use of npm scripts to achieve this so we don’t have to remember all the command line arguments. Ideally, we want to simply run `npm test` and have all the magic happen for us.

Open up your `package.json` file and look for the `scripts` object. Copy the following:

    "scripts": {
      "test": "jest",
      "watch-test": "jest --watchAll"
    },

*Before moving on, let’s have a closer look at our test npm test tasks:**

The watch-test provides us with our TDD runner :+1:

## Writing our first test

In proper TDD fashion, let’s write the first test for a function that adds two numbers.

Let’s create the test file: `touch ./test/sum.test.js`

The tests are written in the traditional _“describe and expect”_ fashion. If we were to write the simplest of a passing test, we could do the following:

```

const sum = require('../src/sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});

```

Let's run our shinny new test and we will get an error

`npm watch-test`

Now lets write the minimal code to make our test pass

Let’s create the file for our function: `touch ./src/sum.js`

The write the function which could look something like following:

```

function sum(a, b) {
  return a + b;
}
module.exports = sum;

```

And that is our first test and function done :+1:

## Lets continue and TDD a React component
If you are just getting started with React, I recommend using [Create React App](https://github.com/facebookincubator/create-react-app). It is ready to use and ships with Jest! You don't need to do any extra steps for setup, and can head straight to the next section. But for the purpose of this demo will go the old fashion way and install the dependencies manually.

## Dependencies and project structure

First off, we know we are going to make use of ES2015 JavaScript syntax. For this to work, we need to install Babel and its dependencies so we can transpile the code, both for the source and our tests. So let’s grab our dependencies, also installing React in the process:

`npm install --save-dev jest babel-jest babel-preset-es2015 babel-preset-react react-test-renderer`

That was a lot of dependencies! All we’re doing is grabbing all the presets so we can teach Babel to expect React and JSX syntax, as well as ES2015 code. We’ll wire things up by creating a `.babelrc` file in the root folder:

`touch .babelrc`

In this file, copy and paste the following configuration for our project:

    {
      "presets": ["react", "es2015"]
    }


This ensures Babel knows how to handle JSX and the ES2015 syntax we’re writing. Note that we could also have done this in the Webpack configuration file, but I personally prefer to keep this kind of configuration separate from the actual build scripts.

Next let's install the REACT dependencies and enzyme to render the components:

`npm install react react-dom enzyme`

## Writing our first test

In proper TDD fashion, let’s write the first test. We’ll write a simple component which has a checkbox which swaps between two labels.

Let’s create the test file: `touch ./test/checkbox.test.js`

The tests are written in the traditional _“describe, expect”_ fashion. If we were to write the simplest of a passing test, we could do the following:

```

import React from 'react';
import {shallow} from 'enzyme';
import CheckboxWithLabel from '../CheckboxWithLabel';

test('CheckboxWithLabel changes the text after click', () => {
  // Render a checkbox with label in the document
  const checkbox = shallow(
    <CheckboxWithLabel labelOn="On" labelOff="Off" />
  );

  expect(checkbox.text()).toEqual('Off');

  checkbox.find('input').simulate('change');

  expect(checkbox.text()).toEqual('On');
})

```

**Notice that we don’t declare `expect` or `shallow`** in this file. Notice that for this, we’re using `shallow()` from enzyme’s API. Checking for types and classes, we don’t actually need to mount or render the components, so shallow is more than good enough here. For more rendering options look at enzyme’s [API](https://github.com/airbnb/enzyme/blob/master/docs/api/). It gives us three separate ways of rendering a component, so it’s not always clear which one we need for our tests.

If we run `npm test` now, our test will fail because we still haven’t written our component. 

So let’s make it pass!!

Let's create `src/components/CheckboxWithLabel.js`

## Create Checkbox with label Component

```

import React from 'react';

export default class CheckboxWithLabel extends React.Component {

  constructor(props) {
    super(props);
    this.state = {isChecked: false};

    // bind manually because React class components don't auto-bind
    // http://facebook.github.io/react/blog/2015/01/27/react-v0.13.0-beta-1.html#autobinding
    this.onChange = this.onChange.bind(this);
  }

  onChange() {
    this.setState({isChecked: !this.state.isChecked});
  }

  render() {
    return (
      <label>
        <input
          type="checkbox"
          checked={this.state.isChecked}
          onChange={this.onChange}
        />
        {this.state.isChecked ? this.props.labelOn : this.props.labelOff}
      </label>
    );
  }
}

```

Run `npm test` again and our test should pass.

Et voila thats all we have time for folks :+1: