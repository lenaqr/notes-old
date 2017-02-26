---
title: How I Set Up This Site
---

*Update (2017): The [Hakyll tutorial][hakyll-tutorial] now has instructions for using `stack` instead of `cabal-install`, which I think is more currently-recommended, so whenever this post talks about cabal you should probably follow what the tutorial says instead.*

This website is written in Markdown, built with [Hakyll][hakyll], and hosted with [GitHub Pages][gh-pages]. In case it interests anyone else, this is how I got started.

## Cabal sandbox

I use a [Cabal sandbox][sandbox] to install all the dependencies for building the site, including Hakyll. This is how I set it up for the first time:

```
$ mkdir site
$ cd site
$ cabal sandbox init
Writing a default package environment file to
/path/to/site/cabal.sandbox.config
Creating a new sandbox at /path/to/site/.cabal-sandbox
$ cabal install -j hakyll
Resolving dependencies...
Notice: installing into a sandbox located at
/path/to/site/.cabal-sandbox
[...]
Installed hakyll-4.6.3.0
```

## Hakyll template

Then, following the [Hakyll tutorial][hakyll-tutorial], I use `hakyll-init` to create the example site (note that I run it with `cabal exec` because it's installed in the sandbox):

```
$ cabal exec hakyll-init .
Creating ./about.rst
Creating ./css/default.css
Creating ./posts/2012-08-12-spqr.markdown
Creating ./posts/2012-11-28-carpe-diem.markdown
Creating ./posts/2012-12-07-tu-quoque.markdown
Creating ./posts/2012-10-07-rosa-rosa-rosam.markdown
Creating ./templates/archive.html
Creating ./templates/post-list.html
Creating ./templates/default.html
Creating ./templates/post.html
Creating ./contact.markdown
Creating ./site.hs
Creating ./index.html
Creating ./images/haskell-logo.png
Creating site.cabal
```

This creates a skeleton to start with, and from here I can use the Hakyll framework to configure the site, customize the templates, and write new content in markdown.

## Building the site

Continuing with the tutorial, I can build the site by compiling `site.hs` and then running `./site build`. Since I'm using Cabal, I can do this in one step with `cabal run`:

```
$ cabal run build
Package has never been configured. Configuring with default flags. If this
fails, please run configure manually.
Resolving dependencies...
Configuring luanthe-github-io-0.1.0.0...
Preprocessing executable 'site' for luanthe-github-io-0.1.0.0...
[1 of 1] Compiling Main             ( site.hs, dist/build/site/site-tmp/Main.o )
Linking dist/build/site/site ...
Running site...
Initialising...
  Creating store...
  Creating provider...
  Running rules...
Checking for out-of-date items
Compiling
  updated templates/default.html
  updated about.rst
  updated templates/post.html
  updated posts/2012-08-12-spqr.markdown
  updated posts/2012-10-07-rosa-rosa-rosam.markdown
  updated posts/2012-11-28-carpe-diem.markdown
  updated posts/2012-12-07-tu-quoque.markdown
  updated templates/archive.html
  updated templates/post-list.html
  updated archive.html
  updated contact.markdown
  updated css/default.css
  updated images/haskell-logo.png
  updated index.html
Success
```

This generates the static files for the site in the `_site` directory.

## Deploying to GitHub Pages

Since I want to deploy the site to GitHub Pages, I create a repository named `luanthe.github.io` on GitHub, point the `_site` directory to a checkout of it, and push:

```
$ cd _site
$ git init
$ git remote add origin https://github.com/luanthe/luanthe.github.io
$ git add --all
$ git commit -m "Initial commit"
$ git push origin master
```

And that's it!

Now whenever I want to publish a post, I rebuild the site with `cabal run rebuild`, commit the changes, and push again.

## Minor fiddly details

There's one problem with this workflow, which is that `cabal run rebuild` blows away the `_site` directory, including the git repository within it. To prevent this, I move `_site/.git` out of the directory and create a plain text file in its place that tells git where to find it:

```
$ cd _site
$ mv .git ../_site.git
$ echo "gitdir: ../_site.git" > .git
```

Then I add a Hakyll rule that recreates the file when it gets blown away:

```
    create [".git"] $ do
        route idRoute
        compile $ makeItem ("gitdir: ../_site.git" :: String)
```

A second minor detail is that I keep the outer `site` directory in a git repository too, so I need to add a `.gitignore` in the outer directory which has a line for `_site` as well as other build artifacts that I don't want in the repository:

```
.cabal-sandbox
cabal.sandbox.config
dist/
_cache
_site
```

## Further reading

In addition to the official docs for Hakyll and GitHub pages, I found the following blog posts helpful in figuring out the process (and I ultimately went with a combination of their approaches):

* [funloop.org: Using Hakyll with GitHub Pages][funloop]
* [chromaticleaves.com: Haskell Development with Cabal Sandboxes][chromaticleaves]
* [begriffs.com: Create a static site with Hakyll, Github, and Travis CI][begriffs]

[hakyll]: http://jaspervdj.be/hakyll/
[gh-pages]: https://pages.github.com/
[sandbox]: http://coldwa.st/e/blog/2013-08-20-Cabal-sandbox.html
[hakyll-tutorial]: http://jaspervdj.be/hakyll/tutorials/01-installation.html
[begriffs]: http://begriffs.com/posts/2014-08-12-create-static-site-with-hakyll-github.html
[chromaticleaves]: http://chromaticleaves.com/posts/cabal-sandbox-workflow.html
[funloop]: http://funloop.org/post/2013-01-11-using-hakyll.html
