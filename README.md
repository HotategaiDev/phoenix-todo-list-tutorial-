<div align="center">

# `Phoenix` Todo List Tutorial!

A complete beginners tutorial building a Todo List in Phoenix.

[![Build Status](https://img.shields.io/travis/dwyl/phoenix-todo-list-tutorial/master.svg?style=flat-square)](https://travis-ci.org/dwyl/phoenix-todo-list-tutorial)
[![codecov.io](https://img.shields.io/codecov/c/github/dwyl/phoenix-todo-list-tutorial/master.svg?style=flat-square)](http://codecov.io/github/dwyl/phoenix-todo-list-tutorial?branch=master)
<!-- [![HitCount](http://hits.dwyl.com/dwyl/phoenix-todo-list-tutorial.svg)](http://hits.dwyl.com/dwyl/phoenix-todo-list-tutorial) -->

</div>
<br />


## Why? 🤷‍

Todo lists are familiar to most people. <br />
_Building_ a Todo list from scratch is a great way to learn Phoenix.

<br />

## What? 💭

A todo list example created from scratch step-by-step in Elixir/Phoenix.

### Try it on Heroku: [phxtodo.herokuapp.com](https://phxtodo.herokuapp.com)


### TodoMVC

We are using the
[TodoMVC](https://github.com/dwyl/javascript-todo-list-tutorial#todomvc)
CSS to make our UI look good and simplify our code.


<br />

## Who? 👤

This example/tutorial is targeted
at anyone who is learning to Elixir/Phoenix.
We have included _all_ the steps required to build the app.


<br />

## _How_? 🚧


### Before You Start!

Before you attempt to _build_ the Todo List,
make sure you have everything you need installed on you computer.
See:
[prerequisites](https://github.com/dwyl/phoenix-chat-example#0-pre-requisites-before-you-start)

Once you have confirmed that you have Phoenix & PostgreSQL installed,
try running the _finished_ App.


### Run The _Finished_ App on Your `localhost` 💻

_Before_ you start building your own version of the Todo List App,
run the _finished_ version on your `localhost`
to confirm that it works.

Clone the project from GitHub:

```sh
git clone git@github.com:dwyl/phoenix-todo-list-tutorial.git && cd phoenix-todo-list-tutorial
```

Install dependencies and setup the database:

```sh
mix setup
```

Start the Phoenix server:

```sh
mix phx.server
```

Visit
[`localhost:4000`](http://localhost:4000)
in your web browser.




You should see:

# TODO: add screenshot/GIF of todo list home page


Now that you have the _finished_ example app
running on your localhost,
let's build it from scratch
and understand all the steps.



### 1. Create a New Phoenix Project 🆕

In your terminal, create a new Phoenix app using the command:

```sh
mix phx.new app
```

Ensure you install all the dependencies:

```sh
mix deps.get
cd assets && npm install && cd ..
```

Setup the database:

```sh
mix ecto.setup
```

Start the Phoenix server:

```sh
mix phx.server
```

Now you can visit
[`localhost:4000`](http://localhost:4000)
from your web browser.

![welcome-to-phoenix](https://user-images.githubusercontent.com/194400/82494801-11caa100-9ae2-11ea-821d-8181580201cb.png)

Shut down the Phoenix server <kbd>ctrl</kbd>+<kbd>C</kbd>.

Run the tests to ensure everything works as expected:

```sh
mix test
```

You should see:

```sh
Compiling 16 files (.ex)
Generated app app

17:49:40.111 [info]  Already up
...

Finished in 0.04 seconds
3 tests, 0 failures
```

Having established that the Phoenix App works as expected,
let's move on to creating the list!

<br />

### 2. Create `items` Schema

In creating a basic Todo List we only need one schema: `items`.
Later we can add separate lists and tags to organise/categorise
our `items` but for now this is all we need.

Run the following [generator](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Html.html) command to create the  

```sh
mix phx.gen.html Ctx Item items text:string person_id:integer status:integer
```

Strictly speaking we only _need_ the `text` and `status` fields,
but since we know we want to associate items with people
(_later in the tutorial),
we are adding the field _now_.


You will see the following output:

```
* creating lib/app_web/controllers/item_controller.ex
* creating lib/app_web/templates/item/edit.html.eex
* creating lib/app_web/templates/item/form.html.eex
* creating lib/app_web/templates/item/index.html.eex
* creating lib/app_web/templates/item/new.html.eex
* creating lib/app_web/templates/item/show.html.eex
* creating lib/app_web/views/item_view.ex
* creating test/app_web/controllers/item_controller_test.exs
* creating lib/app/ctx/item.ex
* creating priv/repo/migrations/20200521145424_create_items.exs
* creating lib/app/ctx.ex
* injecting lib/app/ctx.ex
* creating test/app/ctx_test.exs
* injecting test/app/ctx_test.exs

Add the resource to your browser scope in lib/app_web/router.ex:

    resources "/items", ItemController


Remember to update your repository by running migrations:

    $ mix ecto.migrate
```

That created a _bunch_ of files.
Some of which we don't strictly _need_.
We could create _only_ the files we _need_,
but this is the "official" way of creating a CRUD App in Phoenix,
so we are using it for speed.
See the commit:
[40d4e8d](https://github.com/dwyl/phoenix-todo-list-tutorial/pull/35/commits/40d4e8dd98bae7c517e9a0b59bc2491f4b3c7a0f)


> **Note**: Phoenix
[Contexts](https://hexdocs.pm/phoenix/contexts.html)
denoted in this example as `Ctx`,
are "_dedicated modules that expose and group related functionality_."
We feel they _unnecessarily complicate_ basic Phoenix Apps,
with layers of "interface" and we _really_ wish we could
[avoid](https://github.com/phoenixframework/phoenix/issues/3832) them.
But given that they are baked into the generators,
and the _creator_ of the framework
[_likes_](https://youtu.be/tMO28ar0lW8?t=376) them
(_regardless of them complicating simple apps and confusing beginners_),
we have a choice: either get on board with Contexts
or _manually_ create all the files in our Phoenix projects.


<br />

### 2.1 Add the `/items` Resources to `router.ex`

Follow the instructions presented by the generator to
add the `resources "/items", ItemController` line to the `router.ex` file.

Open the `lib/app_web/router.ex` file
and locate the `scope "/", AppWeb do` section.
Add the line to the end of the block, e.g:

```elixir
scope "/", AppWeb do
  pipe_through :browser

  get "/", PageController, :index
  resources "/items", ItemController
end
```

Your `router.ex` file should look like this:
[`router.ex#L20`](https://github.com/dwyl/phoenix-todo-list-tutorial/blob/f66184b58b7dd1ef593680e7a1a446247909cae7/lib/app_web/router.ex#L20)

<br />

### 2.2 _Run_ The App!

At this point we _already_ have a functional Todo List
(_if we were willing to use the default Phoenix UI_).
Try running the app on your `localhost`:

```
mix phx.server
```

Visit: http://localhost:4000/items/new
and input some data.

![todo-list-phoenix-default-ui](https://user-images.githubusercontent.com/194400/82673112-3edd9780-9c39-11ea-84d3-f62c3e456a6b.png)

Click the "Save" button
and you will be redirected to the "show" page:
[/items/1](http://localhost:4000/items/1)

![todo-list-phoenix-default-ui-show-item](https://user-images.githubusercontent.com/194400/82674191-d7c0e280-9c3a-11ea-9c52-9a37525d0626.png)

This is not an attractive User Experience (UX),
but it _works_!
Here is a _list_ of items; a "Todo List":

![todo-list-phoenix-default-ui-show-items-list](https://user-images.githubusercontent.com/194400/82674676-967d0280-9c3b-11ea-999f-bf5fbe1ab2d4.png)


Let's improve the UX by using the TodoMVC CSS!

<br />

### 3. Create the TodoMVC UI/UX

To recreate the TodoMVC UI/UX,
let's borrow the code directly from the example.



Visit: http://todomvc.com/examples/vanillajs
and inspect the source.
e.g:

![todomvc-view-source](https://user-images.githubusercontent.com/194400/82698634-0b176780-9c63-11ea-9e1d-7aa6e2328766.png)

Right-click on the source you want and select "Edit as HTML":

![edit-as-html](https://user-images.githubusercontent.com/194400/82721624-b8679b00-9cb6-11ea-8d3f-2405f2bd301f.png)


Once the `HTML` for the `<section>` is editable,
select it and copy it.

![todomvc-html-editable-copy](https://user-images.githubusercontent.com/194400/82721711-b05c2b00-9cb7-11ea-85c2-083d2981440d.png)


The `HTML` code is:


```html
<section class="todoapp">
  <header class="header">
  	<h1>todos</h1>
  	<input class="new-todo" placeholder="What needs to be done?" autofocus="">
  </header>
  <section class="main" style="display: block;">
  	<input id="toggle-all" class="toggle-all" type="checkbox">
  	<label for="toggle-all">Mark all as complete</label>
  	<ul class="todo-list">
      <li data-id="1590167947253" class="">
        <div class="view">
          <input class="toggle" type="checkbox">
          <label>Learn how to build a Todo list in Phoenix</label>
          <button class="destroy"></button>
        </div>
      </li>
      <li data-id="1590167956628" class="completed">
        <div class="view">
          <input class="toggle" type="checkbox">
          <label>Completed item</label>
          <button class="destroy"></button>
        </div>
      </li>
    </ul>
  </section>
  <footer class="footer" style="display: block;">
  	<span class="todo-count"><strong>1</strong> item left</span>
  	<ul class="filters">
  		<li>
  			<a href="#/" class="selected">All</a>
  		</li>
  		<li>
  			<a href="#/active">Active</a>
  		</li>
  		<li>
  			<a href="#/completed">Completed</a>
  		</li>
  	</ul>
  	<button class="clear-completed" style="display: block;">Clear completed</button>
  </footer>
</section>
```

Let's convert this `HTML` to an Embedded Elixir
([`EEx`](https://hexdocs.pm/eex/EEx.html)) template.


> **Note**: the _reason_ that we are copying this `HTML`
from the browser inspector instead of _directly_ from the source
on GitHub:
[`examples/vanillajs/index.html`](https://github.com/tastejs/todomvc/blob/c50cc922495fd76cb44844e3b1cd77e35a5d6be1/examples/vanillajs/index.html#L18)
is that this is a "single page app",
so the `<ul class="todo-list"></ul>`
only gets populated in the browser.
So copying it from the browser Dev Tools
is the easiest way to get the _complete_ `HTML`.



### 3.1 Paste the HTML into `index.html.eex`

Open the `lib/app_web/templates/item/index.html.eex` file
and scroll to the bottom.

Then (_without removing the code that is already there_)
paste the `HTML` code we sourced from TodoMVC.



TodoMVC without the TodoMVC styles:
![before-adding-css](https://user-images.githubusercontent.com/194400/82725401-af85c200-9cd4-11ea-8717-714477fc3157.png)


### 3.2 Add TodoMVC CSS


```
<link rel="stylesheet" href="https://todomvc-app.herokuapp.com/lib/todomvc-common-base.css">
<link rel="stylesheet" href="https://todomvc-app.herokuapp.com/lib/todomvc-app.css">
```



<br />

## Learning

+ Learn Elixir: https://github.com/dwyl/learn-elixir
+ Learn Phoenix https://github.com/dwyl/learn-phoenix-framework
