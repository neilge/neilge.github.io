---
title: Webpack
date: 2017-08-10 00:14:17
tags: [Webpack,ES6]
---


**webpack is a module bundler**

By stating what dependencies a module needs, webpack can use this information to build a dependency graph. It then uses the graph to generate an optimized bundle where scripts will be executed in the correct order. Also unused dependencies will not be included in the bundle.

## What are loaders?
Loaders are transformations that are applied on a resource file of your app. They are functions (running in node.js) that take the source of a resource file as the parameter and return the new source.

For example, you can use loaders to tell webpack to load CoffeeScript or JSX.

```js
	module: {
		loaders: [
			{
				test: /\.json$/,
				include: __dirname + '/client',
				loader: 'json-loader'
			},
			{
				test: /\.js$/,
				exclude: /node_modules/,
				loaders: ['react-hot', 'babel']
			}
		]
	}
```

## What is JSX
JSX is a preprocessor step that adds XML syntax to JavaScript. You can definitely use React without JSX but JSX makes React a lot more elegant.

Just like XML, JSX tags have a tag name, attributes, and children. If an attribute value is enclosed in quotes, the value is a string. Otherwise, wrap the value in braces and the value is the enclosed JavaScript expression.

```jsx
	<div className="red">Children Text</div>;
	<MyCounter count={3 + 5} />;

	// Here, we set the "scores" attribute below to a JavaScript object.
	var gameScores = {
	  player1: 2,
	  player2: 5
	};
	<DashboardUnit data-index="2">
	  <h1>Scores</h1>
	  <Scoreboard className="results" scores={gameScores} />
	</DashboardUnit>;
```
