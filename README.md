# NOTE
This guide is a WIP. You can review the final app's code here: [https://glitch.com/edit/#!/project/choo-animals](https://glitch.com/edit/#!/project/choo-animals)

# your first choo app
This page will guide you through your first steps as you build an interactive web app with `choo`.

## Who is this for?
If you're comfortable with the basics of JavaScript, but you've never built an interactive web app before, this guide is for you.

If you are a seasoned JavaScript developer with experience in other frameworks, and are looking to try `choo` for the first time, this guide is also for you.

## Requirements
This guide will assume you are comfortable with the basics of JavaScript, HTML, and CSS.

## What is choo?
`choo` is a small framework that helps you build web apps with JavaScript.

JavaScript makes it easier to add fun interactive elements to our HTML pages. As the language has gained in popularity, developers are now choosing to build their websites entirely with JavaScript. This offers many benefits to both users and developers, most notably that websites can now behave similarly to native desktop or mobile applications.

`choo` provides a small but powerful collection of tools that commonly feature in JavaScript web apps, such as templating, routing, and state management. By the end of this guide, you will understand what these terms mean. Don't be concerned if you don't already know what they are. This is why you are here! :)

## What will we build?
Today we're going to build an interactive animal simulator called `choo animals`. It will be informative, cute, but most of all, fun!

This is what it looks like:

[![screenshot](animals.gif)](https://choo-animals.glitch.me)

The user can click anywhere on the grass to add an animal to the field. Clicking on an animal will remove it from the field. The user can also filter which animals they see, using the filter links at the bottom of the page.

You can try it for yourself here: [https://choo-animals.glitch.me](https://choo-animals.glitch.me)

## Let's get started!
For this guide, we will be using an online code editor called [Glitch](https://glitch.com/).

Glitch lets us write, edit and deploy JavaScript code in the browser. This is useful because we can make changes to our code and see the updated results instantly.

A starter project is available for you to follow along with this guide: [https://glitch.com/edit/#!/project/choo-animals-starter](https://glitch.com/edit/#!/project/choo-animals-starter)

When the editor has finished loading, you should make your own copy of the project so you can begin editing it. To do this, click the `Remix this` button near the top left hand corner of the window:

![remix](remix-this.png "Screenshot of remix this button")

Your screen should now looking something like the following:

![starter](starter-readme.png "Screenshot of starter code")

## Starting choo
In our project's left sidebar, click on the `index.js` file to open its code in the code editor.

You will see the following:

```js
// import choo
var choo = require('choo')

// initialize choo
var app = choo()

// start app
app.mount('div')
```

At the top of this file, we are importing the `choo` framework into our project using the `require()` function.

`require()` lets us import other JavaScript files into our code. `require()` does a lot more than this, but if you're not already familiar with its concepts, for this tutorial all you need to remember is that we will use it to import `choo`, and a handful of other files we write ourselves into our application.

We then need to create an instance of `choo` that we build our app with. We initialize this instance using `choo()`, and then store it in the `app` variable. From this point onwards, when we interact with choo, it will be via `app`.

Finally, we start our application by appending it on onto the `<div>` element of the HTML page our app will run on. We do this using the `app.mount()` method that `choo` conveniently makes available to us. If you open the `index.html` file, you'll see there is a single `<div>` element inside `<body>`. This is where `app.mount()` attaches our code onto.

At this point, we can take a look at what our app currently looks like.

To do this, press the `Show` button near the top left hand corner of the window:

![show](show.png "Screenshot of show button")

A new browser window will open showcasing our application. However, as you'll see, the screen will be blank:

![blank](starter-blank.png "Screenshot of blank browser")

Our application does not yet contain any templates, or any routes. This means that if we try to run our application, we will only ever see a blank page.

Let's fix this.

## Building a template
In web app development, a template often refers to a piece of code that will help us render some HTML to the screen. Being templates, they will render most of the same information each time, but change slightly depending on the different bits of input they receive.

Templates are essentially functions: given some input, they will render a new output depending on what happens inside that function.

`choo` provides another module we can import that will help us build HTML templates with "template strings", one of JavaScript's newer syntax features.

Let's update the code in our `index.js` file to read the following:

```js
// import choo
var choo = require('choo')

// import choo's template helper
var html = require('choo/html')

// initialize choo
var app = choo()

// create a template
var main = function () {
  return html`<div>choo animals</div>`
}

// start app
app.mount('div')
```

Underneath our `choo` import near the top of the file, we're now also importing `choo`'s html helper. This becomes accessible via the `html` variable.

Towards the end of the file, we're creating a function, and assigning it to the `main` variable. Inside the function, we're returning a template that we'll use to render `<div>choo animals</div>` on our page.

This bit of code might be confusing, so let's disect further.

The `html` variable references a function that parses template strings containing HTML code (eg. `` html`<h1>choo</h1>` ``). A given template string will be interpreted into a special data structure, that `choo` then renders as HTML on the page.

## Creating a route
When a friend links you to a specific page on a website, that URL acts as a route so the server knows where to direct you.

Many JavaScript web apps use this same concept to figure out which template to show you at a given point within the application.

This means that to see something on our page, we need to create a route that directs us to the template we just made:

```js
// ...
// initialize choo
var app = choo()

// create a template
var main = function () {
  return html`<div>choo animals</div>`
}

// create a route
app.route('/', main)

// start app
app.mount('div')
```

The `app.route()` function takes in two arguments, the first being the URL path you want to create (this should be specified as a string), and the second being the template you'd like to show users when they arrive at that path (usually a variable that references the template).

As this is our first route, we will make it the "index" (or "root") of the entire application. We do this by specifying the route as `'/'`. This route would be the equivalant of visiting something like `https://choo.io` (the home page). Creating a route with the path `/cats` would be the equivalant of visiting `https://choo.io/cats`.

As we change the code in Glitch's editor, our app's window should automatically update itself. If you open it, you should see the following:

![first route](starter-first-route.png "Screenshot of first route")

If your app hasn't updated yet, you can simply refresh the window yourself.

Now that we can see text on the screen, this means that you successfully got `choo` working! Congratulations :)

We're not finished yet, but let's quickly summarise what we've done so far:

- First, we initialised `choo`, and mounted it onto the page.
- We then created a template using the `choo/html` template function.
- Finally, we created an index route (`/`), and pointed it to our newly made template.

## Modularising our templates
Just like we can `require()` third-party modules like `choo` into our application, we can break our code down into smaller pieces so that the different concerns of our app exist in their own neat little files.

If we were to modularise what we currently have, it would likely be considered "pre-optimisation", since there's not much code there anyway. Attempts to break it out further would likely just increase complexity, but as we're about to add a lot of new markup to our `main` template in just a moment, let's go ahead and break it out into its own file.

In Glitch's left sidebar, click the `+` icon next to `back-end`. Specify your new file's path as `components/main.js`, then click `Add File 👍`:

![new file](starter-new-file.png "Screenshot of new file")

First this creates a new folder named `components`, and then adds a file called `main.js` inside of it. This file should now appear in the sidebar.

Let's add some code to our new `components/main.js` file:

```js
// import choo's template helper
var html = require('choo/html')

// export module
module.exports = function () {
  // create html template
  return html`
    <div class="container">
      <div class="grass">
        <img src="/assets/bg.gif" />
      </div>
    </div>
  `
}
```

What's happening here?

First, we are importing `choo`'s html helper so that we can build a new template within this file.

Next, we are assigning a function that returns a template to the variable called `module.exports`. What does this variable do exactly? In the context of this application, when we create JavaScript files that we'd like to import into other JavaScript files, whatever is assigned to `module.exports` is what will be exported out.

Inside of our template code, we've added some markup that will display an image called `bg.gif` on the page.

__*(NOTE: There are some asset files this project requires that you won't be able to see in Glitch's left sidebar. This image is an example of one those files. Other assets will crop up later in this tutorial, but I'll be sure to point them out to you.)*__

Now let's `require()` this new template into our `index.js` file, and see the results.

Start by adding this line towards the top of `index.js`:

```js
// ...
// import choo's template helper
var html = require('choo/html')

// import template
var main = require('./components/main.js')

// initialize choo
var app = choo()
// ...
```

Underneath the line where we import `choo`'s html helper, we are now importing the `main.js` file we just created. Remembering that we exported a function that returns a template, we can now use that as the designated component for our `/` route.

If we delete the `main` template that's currently located in `index.js`, that file should now look like this:

```js
// import choo
var choo = require('choo')

// import choo's template helper
var html = require('choo/html')

// import template
var main = require('./components/main.js')

// initialize choo
var app = choo()

// create a route
app.route('/', main)

// start app
app.mount('div')
```

If we look at our application, we should now see the following:

![grass](starter-grass.png "Screenshot of grass")

Awesome! Let's recap what we just did:

- First, we created a file called `main.js` inside of a new folder called `components`.
- Inside `main.js`, we created a new template function and then exported it using `module.exports`.
- Finally, we imported `main.js` into `index.js`, and then plugged it into our `/` route.

Now that we have a nice grass field to play in, let's start adding some animals.

## Adding state to our application
A core behaviour of many modern web applications is that they can be entirely driven and interacted with, without having to refresh or navigate to another static HTML page.

When you browse a website like [Wikipedia](https://wikipedia.org) or [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript), each new page you navigate to, or each piece of functionality you interact with, will require a new page from the server to load in your browser.

In `choo`, the idea is that when information is changed or new information becomes available, the page will automatically update itself to reflect that, much in the same way that a native desktop or mobile application would.

To do this, `choo` uses the concept of "application state" to drive the output of its templates. This could mean absolutely nothing to you right now, so it's a good opportunity to dive further into what "state" is and how it works.

In programming, it's commonplace for a script to have several variables which contain information that you pass into a function. A function will typically do the same thing each time you run it, so when you pass the same variables in as arguments again and again, it will keep returning the same result:

```js
var obj = { fun: true, name: 'Alice' }

function sentence() {
  if (fun) {
    console.log(`Yay! ${name} is having fun!`)
  } else {
    console.log(`Oh no, ${name} is not having fun.`)
  }
}

sentence()
sentence()
sentence()

// the following is logged to screen:
// "Yay! Alice is having fun!"
```

As mentioned earlier in this guide:

*"Templates are essentially functions: given some input, they will render a new output depending on what happens inside that function."*

In `choo`, state is passed down into our templates so that we can change what our templates do depending on what is currently contained in that state.

Let's demonstrate this concept by adding new code to our `index.js` file:

```js
// ...

// initialize choo
var app = choo()

app.use(function (state) {
  // initialize state
  state.animals = {type: 'lion', x: 100, y: 200}
}

// declare routes
app.route('/', main)

// ...
```

Underneath our initialization of `choo`, we are calling `app.use()` and passing a function into it. The function we pass in receives a `state` object which represents the state of our entire application. Although it has a wider scope of usage, for now we can just call `app.use()` when we want to setup the initial parameters of our application's state.

Inside of `app.use()`, we're creating a new property on the `state` object called `state.animals`. We're then assigning it an object that contains some parameters we'll use to place a new animal on our screen: `type` sets which animal we want, and the `x` and `y` properties will dictate the animal's position coordinates.

## Passing state into our templates
Now that we've set a new property on our state object, we can access this state from any templates that our router calls.

Let's flip over to `components/main.js`, and update our template function:

```js
// import choo's template helper
var html = require('choo/html')

// export module
module.exports = function (state) {
  var type = state.animals.type
  var x = state.animals.x
  var y = state.animals.y

  // create html template
  return html`
    <div class="container">
      <div class="grass">
        <img src="/assets/bg.gif" />
        <img src="/assets/${type}.gif" style="top: ${x}px; left: ${y}px;" />
      </div>
    </div>
  `
}
```

A few things have changed, so let's briefly dive in to see what's happening:

First, the function that we're exporting now takes in an argument called `state`. This is same `state` object we were dealing with in `index.js`, after it has been run through `app.use()`. This means that the `state.animal` property is now available to us inside this template.

Inside the function, we're initializing a set of variables that point to the different part of our `state.animals` object. Then, inside of our template string, we've created a new `<img>` element. This `<img>` will represent an animal we place on screen. 

As mentioned earlier, we have several different images located inside an invisible `assets` folder in Glitch. They are:

- `assets/bg.gif`
- `assets/crocodile.gif`
- `assets/koala.gif`
- `assets/lion.gif`
- `assets/tiger.gif`
- `assets/walrus.gif`

We can use the `state.animals.type` property that has been passed into our template to point to the correct image we need to render the animal on screen (`src="/assets/${type}.gif"`).

We can then set a `style` property on the same `<img>` element to position the animal using `top` and `left`. These correspond to our `state.animals.x` and `state.animals.y` values.

If we look at our application now, you should see something cute like this:

![first animal](starter-first-animal.png "Screenshot of first animal")

Nice! A super sweet lion has decided to come and hang out with us while we code :)

That was a lot to digest, so let's quickly go over what we just did:

- First, we setup `app.use()` in our `index.js` file.
- Inside of `app.use()`, we then initialized our app's `state` object by describing the type and coordinates of an animal.
- Then, we updated our `main.js` template to reflect the information stored in state.
- As a result, an animal is now rendered on the screen.
