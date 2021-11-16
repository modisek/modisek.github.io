---
title: "My blog setup with hugo and github pages "
date: 2021-11-14T01:19:29+02:00
draft: false
---


I wanted an easy and cheap way to create and host my blog site and hugo came out on top for its ease of setup, and i decided to host it on github pages since it was free.You can find out more about [github pages](https://pages.github.com/) and [hugo](https://gohugo.io/) ,hugo is a static site generator written in GO.

This are the steps i took to host my blog post

#### create and host

- install hugo  following instructions for your distro or operating system 
- install and set up  git/github

- create a new site using the command 
```
hugo new site <name of site>

```

- set up a git repo for your project

```
git init

```
- add theme, more themes can be viewed from here [themes](https://themes.gohugo.io/)


```
git submodule  add <theme>

```

add new content
```
hugo new posts/hello.md

```
run site 

```
hugo server -D

```

create an orphan branch for github pages, using an orphan branch because it will contain simmillar content to the other branch

```
git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m "Init gh-pages branch"
git push origin gh-pages
git checkout main

```

checkout gh-pages, using git worktree to push to multiple branches at once

``` 
git worktree add -B gh-pages public origin/gh-pages

```

push changes to gh-pages

```
cd public 

...

git push

```
set gh-pages as source

setting->pages -> sources select gh-pages

#### automate deployments

``` 
vim .github/workflows/hugo.yml
```
```
name: Hugo

on:
  push:
    branches:
      - main

  # Allows to run workflow manually from Actions tab
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository and update Hugo themes
        uses: actions/checkout@v2
        with:
          submodules: true
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

      - name: Install Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "0.81.0"
          extended: true

      - name: Build Hugo
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```

make a change and commmit it to main to see the workflow being run and your site being deployed
