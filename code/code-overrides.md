# Code Overrides

## Overview

Code overrides allow you to change any Frame or Component on the canvas with code before it shows in the Preview. They can for example:

* Change a visual property like color or opacity.
* Add an interactive event handler with animations.
* Communicate between multiple Frames or Components.
* Handle user input and apply real dynamic data.

Code overrides are simple JavaScript functions you can write yourself and apply to any Frame or Component on your canvas, so they are highly shareable. The functions are simple transformers that get the properties from the canvas as inputs \(props\) and return them with modifications.  
  
Code overrides can live in any code file in your project. They get discovered as they use the `Override` [type specifier](https://www.typescriptlang.org/docs/handbook/basic-types.html) \(see example below\). You can apply any code override to any Frame \(or Component\) on the canvas from the properties panel under “Code”.

The simplest example of a code override is one that sets the background color of a Frame to red, independent of the background you set on the canvas.

```typescript
import { Override } from "framer";

export const makeRed: Override = props => {
  return { background: "red" };
};
```

{% hint style="info" %}
Make sure you setup [VSCode for external editing](https://framer.gitbook.io/framer/~/edit/drafts/-LKS1WMROLkDNccBN9iI/application#setup).
{% endhint %}

## Events

For anything interactive, you need events. Events are “things that happen” like a click, tap, swipe, but also video ended or device rotated. They consist of a type and a handler with code that needs to be run when the event happens.  
  
Because you can’t set event handler from the interface in Framer X \(today\), you need to set them with a code override. Event types in Framer follow the same style as in JavaScript \(or [React](https://reactjs.org/docs/events.html#supported-events)\) like onClick, onTap, onScroll, etc.  
  
Let’s create a very simple event handler that logs a message to the console with `console.log` when you click it.

```typescript
import { Override } from "framer";

export const logTap: Override = props => {
  return { onTap: () => console.log("Hello") };
};
```

Apply the code override to any Frame on the canvas and click it in the preview. If you open the preview console \(right bottom icon in the main window\) you will see multiple “Hello” messages \(in the Console tab\).

{% hint style="info" %}
Many advanced events like pinch and swipe are still missing from the Framer Library in beta 2. They will be added in a future beta.
{% endhint %}

## Animations

The [Framer JavaScript Library](framer.js/) comes with a set of [advanced animation helpers](framer.js/animation.md) for high performant accelerated graphics that work well with Framer X. They work very well with overrides to animate any Frame on your canvas.  
  
Let’s create a code override to animate the scale of a Frame on a click.

```typescript
import { Override, Animatable, animate } from "framer";

const scaleValue = Animatable(1);

export const scaleUp: Override = props => {
  return {
    scale: scaleValue,
    onTap: () => animate.spring(scaleValue, 1.5)
  };
};
```

After we import the right parts from the [Framer Library](framer.js/), we create a new Animatable number called `scaleValue` with a default value of 1. We use this value to set the scale property initially, and we animate it with a spring curve after a click.  
  
You can also separate the animation from the click event so you can click on one Frame and animate another. Just connect the `scaleUp` code override to one of the Frames so it sets the scale property to the `scaleValue` value. Connect the other Frame to `scaleButton`, which animates the `scaleValue` on a click.

```typescript
import { Override, Animatable, animate } from "framer";

const scaleValue = Animatable(1);
let toggle = false;

export const scaleUp: Override = props => {
  return { scale: scaleValue };
};

export const scaleButton: Override = props => {
  return {
    onTap: () => {
      if (toggle) {
        animate.spring(scaleValue, 1);
        toggle = false;
      } else {
        animate.spring(scaleValue, 1.5);
        toggle = true;
      }
    }
  };
};

```

Please note we need to use let for the toggle here as we replace the value when you click to keep track of the state. As a pro tip \(and an exercise for the user\), you can greatly simplify the code inside `onTap` with a [conditional operator](https://stackoverflow.com/questions/6259982/how-do-you-use-the-conditional-operator-in-javascript).

## Application State

Every complex project has a set of parameters \(or variables\); whether the user is logged in, what a choice was on a previous screen, or a downloaded set of friend names. The displayed user interface at any point is a result of all of that data, and any change to it should update the user interface.  
  
The [Framer Library](framer.js/) provides a simple Data object that does exactly that. It behaves like a plain JavaScript object you can store anything in, and it updates your project user interface every time anything changes.  
  
Let’s look at two code overrides that update the text of a Frame when you click another Frame. Start by setting up a new document with a Frame and Text.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_163220D9C0E803228842F5F3CA6BABB8C8965572CBECA3832DE533848A871A26_1534852249638_image.png)

Now let’s write two code overrides, one for the button and one for the text, so the text changes when we click the button.

```typescript
import { Override, Data } from "framer";

const app = Data({ name: "Koen" });

export const useName: Override = props => {
  return {
    text: app.name
  };
};

export const useNameButton: Override = props => {
  return {
    onClick: () => {
      app.name = "Jorn";
    }
  };
};

```

The app variable holds a Data object with the name set to “Koen”. The `useName` sets the text property to the value of the `name`. The `useNameButton` updates the name value to “Jorn”. As soon as it gets updated, you’ll see the user interface reflect it.

