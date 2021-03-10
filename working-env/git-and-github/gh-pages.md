# GH-Pages

## Create a Root GH-Page

* Create a new repo named as `YourAccountName.github.io`, **with a** `README` **in it**.
* Go to this repo setting, finde the botton `Choose theme`, `Select` a theme you like.
* Back to repo, you’ll see a new file named `_config.yml`. Open and add new configs:

  ```yaml
  ---
  title: Your Title
  description: Your Description
  ---
  ```

* Create a file `index.html` or `index.md`.
* Go back to this repository's settings page, check the `Github Pages` block, you can see your site is accessible now.

## Create a Project Under the Root GH-Page

* Create a new repo named as you like.
* Go into the repo, you will see a pulldown button of `Branch: main`. Click it and create a new branch: `gh-pages.`
* Set `gh-pages` as default. Now you can deletet the `main` branch.
* Go into the repository's settings page, find the `Github Pages` block, change the source option to `gh-pages`. Keep it under the `/(root)` , or if you need to put it under another gh-page, you can change it also.
* Select a theme, create index file, and check links as above.

## How to Use GH-Pages to Maintain Blog

* `gh-pages` use `Jekyll` \(but not full\), you can search gh-pages documentation to get help.
* A lazy way to run gh-pages:

  * You can set `settings` in your gh-pages, choose a theme, then run `git pull`.
  * Open `index.html`, and write a line at tht top in `yml` language:

  ```yaml
  ---
  layout: home
  ---
  <!-- No other content here -->
  ```

  * Then, create your first blog as file `_post/yyyy-mm-dd-Your_Title.md`. At the top of the blog, you should write in `yml` language like this:

  ```yaml
  ---
  layout: post
  title: Your Title
  author: Your Name
  ---
  <!-- Here is your content writen in `markdown` -->
  <!-- Search 'Markdown tutorial' in the google, if you don't know how to write markdown -->
  ```

### Advanced

* It is recomended to pull an push between local and remote, because edit markdown in a good local editor is much comfortable than coding in the browser textarea.
* You can customize your domain, just follow gh-pages documentation. You should know the basics of DNS Register and DNS Record.
* You can integrate a lot of plugins to your gh-pages blog, such as add a search page, add a classification, add tags... NOTE: gh-pages will build your pages on their cloud server, you do not need to set up a Jekyll environment locally which will take a lot of effort unless you want to preview your page at the localhost.

  * [https://github.com/jekylltools/jekyll-tipue-search](https://github.com/jekylltools/jekyll-tipue-search)
  * [Deploy Jekyll pages using Git and Travis CI](https://github.com/felixrieseberg/travis-jekyll-git)
  * [Tutorial - Integrating Jekyll and Travis CI](https://tonyzhangnd.github.io/2018/06/Integrating-Jekyll-and-Travis-CI.html)
  * ...
  * An easy way to go is to fork gh-pages template from other developer. But you still should understand the basic HTML and CSS

  > I have built a blog with gh-page on my own, it was the first time I play with GitHub and gh-pages.

  [SHELDON IS ALWAYS LEARNING](https://sheldonldev.github.io/)

  > It really helped me a lot at the very beginning. I got my hand dirty with it, such as pull, push, stash, merge, the markdown syntax, the static website, the template, the YAML syntax... I messed things up and fix it. But now, for more efficiency, I keep notions here.

