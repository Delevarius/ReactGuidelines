# React Code Style Guide

Our React projects' best practices

<br>

# Introduction

This is meant to be a guide to help developers understand
the React code style and best practices we adopt here at Melon.

<br>

# Installing

The rules described in this repository are also *GOING TO BE* available as a NPM package.
NPM PACKAGE LINK AND GUIDE HERE

<br>

# Table of contents

- [Component definition](#component-definition)
- [Project organization](#project-organization)
  - [Presentational Components](#components)
  - [Container Components](#containers)
  - [Page Containers](#pages)

# Component definition

All components (presentation, containers or pages) should **always** be
defined as a directory, named with pascal casing. The main component file
should be `index.js`, main stylesheet `style.css`. 
Constants that are to be used such as switch types in reducer functions, url endpoints etc, should be separated in a file of their own, usually simply named `constants.js`.
Reusable types should be separated in a file of their own, usually simply named `types.js`.
Reusable functions and helper functions used only locally in this in  should be separated in a file of their own, usually named `utils.js`.
All fetch requests made to an external API should be separated in a file of their own, usually simply named `fetch.js`.
:

```
AwesomePage/
├── properties.css
   ├── components/
   ├── RootComponent.jsx
   ├── AnotherComponent.jsx
   ├── YetAnotherComponent.jsx
   ├── constants.js
   ├── fetch.js
   ├── types.js
   ├── utils.js
   ├── index.js
   └── style.css
```

* Styles should always be defined in a separate CSS file
* Avoid prefixing or suffixing component names
  - E.g.: `lib/pages/UserPage` or `lib/container/UserContainer`
* On conflict rename on import time
  - `import UserContainer from '...'`
  - `import { User as UserContainer } from '...'`

[:arrow_up: Back to top][table-of-contents]

# Project organization

Your project components should be separated in such a way that :

```
awesome-react-project/
└── src/
   ├── lib/
   ├── PageOne/
   ├── PageTwo/
   └── index.js
```

Each of these directorie:

### `lib/`

Stateless components. Shouldn't store state. Most components in this
directory will be function-based components. Stuff like buttons, inputs,
labels and all presentational components goes here. This components can
also accept functions as props and dispatch events, but no state should
be held inside.

### `pages/`

Page components can store state, receive route parameters and dispatch
Redux actions when applicable. Pages are the highest level of application's
components. They represent the application routes and most times are
displayed by a router. Pages are also responsible for handling container
components callbacks and flowing data into children containers.

[:arrow_up: Back to top][table-of-contents]

# Code standards

## Destruct your `props`

### More than 2 props from an object been used in the same place should be destructed


## Code style
### Line length should not exceed 80 characters.

### Use explanatory variables
Bad
```js
const onlyNumbersRegex = /^\d+$/
const validateNumber = message => value => !onlyNumbersRegex.test(value) && message

validateNumber('error message')(1)
```

Good
```js
const onlyNumbersRegex = /^\d+$/
const getNumberValidation = message => value => !onlyNumbersRegex.test(value) && message

const isNumber = getNumberValidation('error message')

isNumber(1)
```

### Use searchable names
Bad
```js
setTimeout(doSomething, 86400000)
```

Good
```js
const DAY_IN_MILLISECONDS = 86400000

setTimeout(doSomething, DAY_IN_MILLISECONDS)
```


## Naming

### Test files must start with the class which will be tested followed by `.test`.

### Class and components folders names must start with capital letter.


## React peculiarities

### Never "promisify" the `setState`
It's a small anti-pattern which can cause some problems in the component lifecicle. You can found more arguments about this in [this issue](https://github.com/facebook/react/issues/2642#issuecomment-352135607)

## Mixins
 - [Do not use mixins](https://reactjs.org/blog/2016/07/13/mixins-considered-harmful.html)

 Why? Mixins introduce implicit dependencies, cause name clashes, and cause snowballing complexity. Most use cases for mixins can be accomplished in better ways via components, higher-order components, or utility modules.

## Components 

### One line props when are more than 2 or big props

Bad
```jsx
<button type="submit" disabled onClick={() => null} className="aLongSpecificClassName">
  Click here
</button>

<button type="submit" className="aLongSpecificClassName">
  Click here
</button>

<button className="aLongSpecificClassName">Click here</button>
```

Good
```jsx
<button
  className="aLongSpecificClassNameWithLasers"
  disabled={loading}
  onClick={() => null}
  type="submit"
>
  Click here
</button>
```

### One line component
Bad
``` js
<div className="example"><span class="highlight">Bad</span> example</div>
```

Good
``` js
<div className="example">
  <span className="highlight">Bad</span>
  example
</div>
```





[:arrow_up: Back to top][table-of-contents]

---
