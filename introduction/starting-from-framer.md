# Starting from Framer

## Overview

Framer X is quite different from legacy Framer at first sight. But it builds on everything that made the original Framer great with an improved approach, and solving some long standing problems like package collaboration.

The biggest surface differences are:

* Everything is React and ES6 \(versus CoffeeScript and plain Framer\)
* There is no more built-in code editor inside Framer X.
* There are some visual tools that write code for you \(link, scroll, page\).

We strongly believe Framer X is better than legacy Framer from a prototyper programming perspective. It will allow you to build both very small high fidelity throw away prototypes all the way to production ready complex projects, if you like. The new declarative programming model with components will help you structure and organize your projects, make them easier to reason about for yourself and others, yet is completely optional if you have another preferred way of working.

### Things to Try

These are some things to explore if you are coming from Framer Studio. Make sure you setup [VSCode for external editing](../code/#setup).

* Create a single code component and modify the html and css. Study the `propertyControl` and how you can add properties interface to components.
* Create a `<Frame />` component with an [animated property](../code/code-overrides.md#animations) via a [code override](../code/code-overrides.md), an `onClick` [event](../code/code-overrides.md#events) and use the `animate()` function to animate the property.
* Use a design component with custom properties from the canvas in a code component and [use it in a loop](../components/design.md#exporting-importing-from-code).
* Use a code component on the canvas and use a [code override with state](../code/code-overrides.md#application-state) and an event handler modifying the state.

### JavaScript \(ES6\)

Lots of people love CoffeeScript. It's a nice layer on top of JavaScript that encourages you to use the "[good parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)" of JavaScript. But we originally mainly picked CoffeeScript because we found out it looked a lot "less intimidating" to aspiring new programmers. That is mostly due to brackets being optional, relying on whitespace \(like tabs and spaces\) for the language structures. In practice, we found a trade off when people continued learning the language. For example, it's hard to sport errors in whitespace \(because it's invisible\), plus allowing for multiple ways to write the same thing can lead to confusion and makes code harder to read.

But the main reason for switching is that JavaScript has been improving while we were using CoffeeScript. With the latest version ES6, it fixes a lot of things that CoffeeScript was originally designed for \(often inspired by CoffeeScript\) plus a [whole lot more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) that CoffeeScript could never do as a layer on top of JavaScript.

### React and Components

Everything in Framer X is based on React, a popular but very minimal interface framework for JavaScript. And while there are many different flavors of those, the main things Framer uses React for is:

* A set of agreements to describe components.
* A structured, _declarative_ way to reason about your interface.

These ideas are the things that make React great \(and so popular\). They're not new and will be around for a long time, independent of the implementations of the ideas \(the specific framework\). So just think of React as a set of great ideas to build interfaces.

Additional great reasons to build on React are that it's _extremely easy to learn_, if you know basic web development \(html and css\) it's enough to build your own component. Plus, if you happen to work at a place that uses React in production too, there is a chance you can efficiently share code.

#### Components

Legacy Framer projects had no structure by default and that made it very hard to re-use, compose or share parts of your interface, within and between projects.

#### Declarative vs Imperative

Legacy Framer was mostly imperative, while Framer X is fully declarative. These words entail a philosophical different way of describing a change in the world. I'll try to explain.

_Imperative_ is like a cooking recipe. It describes a set of steps and ingredients that, if followed correctly, lead to a great dish at the end. It may allow for some variation, but it's important to follow all the steps closely, or the end state might be unexpected.

_Declarative_ focuses purely on describing the dish and leaves it up to the maker to figure out how to get there, as long as it ends up in a certain way.

Computers are really great at figuring out steps between different states. So describing your interfaces declaratively and leaving the steps up to the computer is a great idea for building interfaces. This way you can just describe your states \(loading, error, login screen\), under which conditions to show them, and let the computer figure out the rest.

