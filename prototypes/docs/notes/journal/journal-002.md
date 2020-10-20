# Journal 001: How might this thing work, again?

## Goals/Requirements

I have some:

* It should be really easy for anyone using bfeed to migrate their site somewhere else
  * Like, *really* easy
* I’d like to retain the history of all changes to each site
* I want the sites to be as isolated from each other as possible
* I want the sites to be served as static files, via a CDN
* I want to “outsource” as much as possible to managed services.

## Architectural Overview

Here’s an overview of what I have in mind, in broad strokes:

* The “source” content for each site will be a Git repo hosted at GitHub
* The “live” incarnation of each site will be a static site built and hosted by Netlify
* Every time someone uses the app to publish a change to their content:
  1. The app pushes that change to the GitHub repo
  2. GitHub notifies Netlify about the change via a Webhook
  3. Netlify builds/rebuilds the site and publishes the site to its CDN
* A site could have thousands of posts, and the app will need to be able to list and
  search the posts (at first, searching by title alone should be OK, maybe?)
  * So the app will also maintain an index file in the repo
  * Maybe an SQLite DB?
  * SQLite can also do full-text search — so maybe include the full content of each article in there as well?
 
## Some open questions

* What Static Site Generator (SSG) should we use?
  * Hugo seems mature and fast, and supports themes, so let's maybe start with that
  