<div align="center">

# `Phoenix` Todo List Tutorial!

A complete beginners tutorial building a Todo List in Phoenix.

[![Build Status](https://img.shields.io/travis/dwyl/elixir-invoke-lambda-example/master.svg?style=flat-square)](https://travis-ci.org/dwyl/elixir-invoke-lambda-example)
[![codecov.io](https://img.shields.io/codecov/c/github/dwyl/elixir-invoke-lambda-example/master.svg?style=flat-square)](http://codecov.io/github/dwyl/elixir-invoke-lambda-example?branch=master)
[![HitCount](http://hits.dwyl.com/dwyl/elixir-invoke-lambda-example.svg)](http://hits.dwyl.com/dwyl/elixir-invoke-lambda-example)

</div>
<br />


## Why? 🤷‍

Todo lists are familiar to most people. <br />
Building a Todo list from scratch is a great way to learn Phoenix.
You can learn to navigate the folders & files of a _boring_
Phoenix App that you _already_ understand.



## What? 💭





### Try it on Heroku:




## Who? 👤

This example/tutorial is targeted
at anyone who is new to Elixir/Phoenix.




### Run it on your `localhost`

Clone the project from GitHub:

```sh
git clone git@github.com:dwyl/phoenix-todo-list-tutorial.git
```





## How? 💻

Now that you have the _finished_ example app
running on your localhost,
let's build it from scratch
and understand all the steps.



### 1. Create a Phoenix Project 🆕

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

![phoenix-default-homepage](https://user-images.githubusercontent.com/194400/74361992-c2c4ef80-4dbf-11ea-8112-2dcf6dcf1c51.png)

Also make sure you run the tests to ensure everything works as expected:

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

Having established that your Phoenix App works as expected,
let's dive into the fun part!






## Learning

+ Learn Elixir: https://github.com/dwyl/learn-elixir
+ Learn Phoenix https://github.com/dwyl/learn-phoenix-framework
+ Learn Vagrant: https://github.com/dwyl/learn-vagrant
