# React (+TypeScript) with React's Context API TodoMVC Example

An implementation of [TodoMVC](http://todomvc.com/), that is written with the use of React's new Context API.

## Running the example

```
npm install
npm start
```

## Code structure

We have contexts defined in the `contexts` folder, and components in the `components` folder.

## Some background on React Redux

With React, application developers began preferring a single sources of truth to be placed on the highest level component in the dependency tree, and have parts of the truth trickle down to child components. The parent component is also responsible to pass event handlers to children.

When an event is triggered by a child component, the event needs to bubble up.

However, this yields potentially tightly coupled code. A change in the interface on a child component requires that the parent component adapts.

And so, React Redux was introduced to mitigate this.

With React Redux, the "provider" component is what responds to changes to the store, and it is also what passes state to child "Container" components. "Container" components are what gets the current state and event handlers from the store. There can exist multiple container components, none of which require that a parent component pass state down to the children.

## How context differs from React Redux

With contexts, we are introduced to two new components generated by React. These are the "producer" and the "consumer".

With these components rendered somewhere higher up on the render, child components are free to declare their render tree to include a consumer that will inject the producer's "properties".

The first difference here is that we are now explicit in what is injected into a "container" components. This yields code that is much easier to reason about. Indeed, in TypeScript, we are no longer bounded to defining exclusively "optional" properties passed-in to container components, which is ideal, since we don't want them to be defined as optional.

Other than the manner in which state is passed to children, the other difference is that we are freed from having to initialize a separate "store" to hold our application state. We instead let it be a part of a parent component's state lifecycle. The only con, here, is that we lose out on the ability to debug any state-updating events via [Redux DevTools Chrome extension](https://github.com/zalmoxisus/redux-devtools-extension).

However, although we are no longer required to initialize a store (unlike in React Redux), we are still free to *use* any state-management systems, such as ([plain-vanilla](https://en.wikipedia.org/wiki/Plain_vanilla)) Redux. A complement to using Redux is that we are free to respond to state change however we wish.

Nevertheless, Redux was not used in this application, since it was purely meant as a demonstration on the use of React's new context api.