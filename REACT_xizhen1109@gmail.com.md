# Topic: React

**Author**: XuXiZhen

**Conact EMail**: xizhen1109@gmail.com

**QAs Total**: 3

---

## Q1: What's the difference between `class based components` vs `functional components` in React?

**Difficulty:** `Junior`

**Source**:

https://stackoverflow.com/questions/51054940/class-based-component-vs-functional-components-what-is-the-difference-reactjs

**Answer**:

Class Components:

- Class-based Components uses ES6 class syntax. It can make use of the lifecycle methods.
- As you can see in the example that u have given above Class components extend from React.Component.
- In here you have to use this keyword to access the props and functions that you declare inside the class components.

Functional Components:

- Functional Components are simpler comparing to class-based functions.
- Functional Components mainly focuses on the UI of the application, not on the behavior.
- To be more precise these are basically render function in the class component.
- Functional Components can't have state and they can't make use of lifecycle methods.

---

## Q2: What's the difference between `React Context` vs `React Redux` in React?

**Difficulty:** `Mid`

**Source**:

https://stackoverflow.com/questions/49568073/react-context-vs-react-redux-when-should-i-use-each-one

**Answer**:

As `Context` is no longer an experimental feature and you can use Context in your application directly and it is going to be great for passing down data to deeply nested components which what it was designed for.

As Mark Erikson has written in his blog:(http://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/)
```
  If you're only using Redux to avoid passing down props, context could replace Redux - but then you probably didn't need Redux in the first place.
  Context also doesn't give you anything like the `Redux DevTools`, the ability to trace your state updates, `middleware` to add centralized application logic, and other powerful capabilities that `Redux` enables.
```

`Redux` is much more powerful and provides a large number of features that the Context API doesn't provide, also as @danAbramov mentioned:
```
  React Redux uses context internally but it doesn’t expose this fact in the public API. So you should feel much safer using context via React Redux than directly because if it changes, the burden of updating the code will be on React Redux and not you.
```

Its up to Redux to actually update its implementation to adhere with the latest Context API.

The latest Context API can be used for Applications where you would simply be using Redux to pass data between components, however applications which use centralised data and handle API request in Action creators using `redux-thunk` or `redux-saga` still would need Redux. Apart from this Redux has other libraries associated with it like `redux-persist` which allows you to save/store data in localStorage and rehydrate on refresh which is what the Context API still doesn't support.

As @dan_abramov mentioned in his blog You might not need Redux, Redux has useful applications like:
```
  - Persist state to a local storage and then boot up from it, out of the box.
  - Pre-fill state on the server, send it to the client in HTML, and boot up from it, out of the box.
  - Serialize user actions and attach them, together with a state snapshot, to automated bug reports, so that the product developers
    can replay them to reproduce the errors.
  - Pass action objects over the network to implement collaborative environments without dramatic changes to how the code is written.
  - Maintain an undo history or implement optimistic mutations without dramatic changes to how the code is written.
  - Travel between the state history in development, and re-evaluate > the current state from the action history when the code changes, ala TDD.
  - Provide full inspection and control capabilities to the development tooling so that product developers can build custom tools for their apps.
  - Provide alternative UIs while reusing most of the business logic.
```

With these many applications its far too soon to say that Redux will be replaced by the new Context API.

Consider:

`Redux`

![](https://res.cloudinary.com/academind-gmbh/image/upload/f_auto,q_auto:eco/dpr_2.0,w_400,c_limit,g_center/v1/academind.com/content/tutorials/reactjs-redux-vs-context-api/redux-overview)

`Context`

![](https://imgs.developpaper.com/imgs/1125940358-5fd723259016a_fix732.png)

---

## Q3: What are `synthetic events` in React?

**Difficulty**: `Senior`

**Source**:

https://blog.logrocket.com/a-guide-to-react-onclick-event-handlers-d411943b14dd/

**Answer**:

A synthetic event is a cross-browser wrapper around the browser’s native event. It has the same interface as the browser’s native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers.

It achieves high performance by automatically using event delegation. In actuality, React doesn’t attach event handlers to the nodes themselves. Instead, a single event listener is attached to the root of the document. When an event is fired, React maps it to the appropriate component element.

**Details**:

Provide some synthetic events example directly inside an `onClick` event handler

**Detail Answer**:

You can also use synthetic events directly inside an `onClick` event handler. In the example below, the button’s value is gotten via `e.target.value` and then used to alert a message.

```js
import React from "react";

const App = () => {
  return (
    <button value="Hello!" onClick={(e) => alert(e.target.value)}>
      Say Hello
    </button>
  );
};

export default App;
```
