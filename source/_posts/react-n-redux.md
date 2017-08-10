---
title: React and Redux
date: 2017-08-10 00:08:11
tags: [React,Redux]
---


Origin Resourse from [Building a Simple CRUD App with React + Redux](http://www.thegreatcodeadventure.com/building-a-simple-crud-app-with-react-redux-part-1/)

## The advantage of React

React is fast. It uses the virtual DOM to track the state of the actual DOM, only re-rendering discrete sections of the DOM as changes to application state dictate.

But where I really started to see the advantages of React was in the flow of data through the application, in the purely Data Down Actions Up system of maintaining application state.

In React, your components can have both state and properties. A component's properties should be considered **immutable**. Instead of a component responding to a user's action by updating it's own properties, it will send an action that updates the entire application's state, which in turn triggers a re-render of a component, updating that component's properties as a result.

![state and props](/2017/08/10/react-n-redux/react-diagram.png)
