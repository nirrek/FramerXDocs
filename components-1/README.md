# Components

## Conceptual

Components are like legos for your interface. They are small building blocks that you can compose into larger ones, making up entire screens, interfaces and apps.

As a designer, you might have different definitions of components as most visual tools treat components as pictures of real components. In Framer X, the components are all real. They scroll, click, move and handle input, all backed by the popular React JavaScript framework for building interfaces.

_PS: Please Lego don't sue me for this analogy._

## Types of Components

Framer X has two types of components, which it treats the same because they ultimately are the same under the hood: React components:

* \*\*\*\*[**Design components**](design-components-wip.md) – components that you draw on the canvas consisting of visual and basic interaction that you can express on the canvas. Everyone can build these. Design components are fully editable on the canvas.
* \*\*\*\*[**Code components**](code-components.md) – components that are backed by code with React. They can be anything from simple HTML and CSS all the way to advanced JavaScript, optionally building on other libraries again. Code component are only editable from code, but they can display other Frames from the canvas via the children prop or canvas imports \(more below\).

Any component can be displayed on the canvas, but interactive components \(like scroll or something with a click\) only work in the Preview. Both design and code components can be composed into any hierarchy on the canvas, design components can even contain code components, and every component has the same automatic layout options as any Frame.

A Framer X project lists all components in that specific project under the Components tab on the left. The components can origin from:

* Your project canvas \(design components\).
* Your project code \(code components\).
* Installed packages \(either types\).

## 

