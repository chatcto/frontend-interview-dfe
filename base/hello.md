# hello

hi shudong

## How It Works

A VuePress site is in fact a SPA powered by [Vue](http://vuejs.org/), [Vue Router](https://github.com/vuejs/vue-router) and [webpack](http://webpack.js.org/). If you've used Vue before, you will notice the familiar development experience when you are writing or developing custom themes (you can even use Vue DevTools to debug your custom theme!).

During the build, we create a server-rendered version of the app and render the corresponding HTML by virtually visiting each route. This approach is inspired by [Nuxt](https://nuxtjs.org/)'s `nuxt generate` command and other projects like [Gatsby](https://www.gatsbyjs.org/).

Each markdown file is compiled into HTML with [markdown-it](https://github.com/markdown-it/markdown-it) and then processed as the template of a Vue component. This allows you to directly use Vue inside your markdown files and is great when you need to embed dynamic content.

## Features

**Built-in markdown extensions**