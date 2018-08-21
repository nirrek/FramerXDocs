# Animation

## Overview

In Framer X, you animate _values_ instead of _objects_. A value can be a number, color or even string. If you use these values on any Framer component \(like the left property of a Frame\) they will animate very efficiently.

The programming API for Framer Animations are loosely based on the standard [Web Animation API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API). It consists of the following parts:

* **Animatable values**: the values that can be animated: number,  color and string.
* **Animation function**: the animate function to create new animations for any value with options like curve and duration.
* **Animation curves**: curves for different animations like linear, spring or bezier.
* **Animation object**: the actual animation that you can control with play, pause and reverse.
* **Animation events:** things that happen to animations like start, finish and cancel.

_**Note**: the Framer animation approach is loosely based on_ [_React Native Animated_](https://facebook.github.io/react-native/docs/animated)_._

## Usage

Let’s look at the simplest example to use a Framer Animation, this should look fairly familiar if you have done any web development before.

```typescript
import * as React from "react";
import { Frame, Animatable, animate } from "framer";

export class Example extends React.Component {
  aLeft = Animatable(0);
  render() {
    return <Frame left={this.aLeft} onClick={() => animate(this.aLeft, 200)} />;
  }
}
```

This builds a simple React component with just a single `Frame`, that has the left property bound to an animatable value this.aLeft \(something I made up\). The default value is 0. The onClick handler on the Frame uses the animate function to animate the value to 200, with a default linear curve and duration of one second.

## Curves

In the example above, we did not set any animation options, so it uses the default ease curve:

```typescript
animate(this.aLeft, 200)
```

If we would like the spring curve with options we simply use it like this:

```typescript
animate.spring(this.aLeft, 200, {tension: 400})
```

There are a couple curves available:

* `linear` , `ease`, `easeIn`, `easeOut`, `easeInOut` with options `{duration: 1}`
* `spring` with options `{tension: 10, friction: 100}`
* `bezier` with options `[0, 0, 1, 1]` or `Bezier.Ease`

## Events

Events provide a powerful way to respond to changes in animations. This way you can build sequences or build non-linear flows, like when a user interrupts an animation.

Events in Framer use a [modern JavaScript feature](https://medium.com/front-end-hacking/callbacks-promises-and-async-await-ad4756e01d90) called async and await. They are powerful primitives but you can simply think of them as ways to “wait until something happens” like an animation ending or being interrupted.

Let’s look at a simple example that waits for one animation to finish and then immediately starts a new one so it ends up where it began. We’ll use the async and await constructs to wait for the finished state.

```typescript
import * as React from "react";
import { Frame, Animatable, animate } from "framer";

export class Example extends React.Component {

  left = Animatable(0);

  onClick = async () => {
    await animate(this.left, 200).finished
    await animate(this.left, 0).finished
  };

  render() {
    return <Frame left={this.left} onClick={this.onClick} />;
  }
}
```

When using `await` your function has to be marked `async`. This is how JavaScript works, so notice `async` next to the `onClick` function. From there you can see we use `await` with `.finished` on the animation to wait before running the next line of code, so that the animation only starts with the previous one is done. If you were to remove the await keywords, both animations would start immediately.

The other available events are:

* `ready` – The animation is ready to start \(this happens automatically if you use the `animate()` function.
* `finished` – The animation finished completely.

## Technical Information

* Animations only work with Framer components \(as we directly modify the DOM\).
* Animations are technically observables, much like [React Animated](https://facebook.github.io/react-native/docs/animated).
* Animations directly modify the DOM for performance, so they don’t trigger React tree diffs.
* Animations in Framer are cross browser compatible from IE8 and up.

