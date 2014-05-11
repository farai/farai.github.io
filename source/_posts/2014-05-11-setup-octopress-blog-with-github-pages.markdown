---
layout: post
title: "Setup Octopress blog with Github Pages"
date: 2014-05-11 10:48:30 +0100
comments: true
categories:
---

Having decided to start blogging again after a minor hiatus I've decided to start a new blog using [Octopress](http://octopress.org/) as the framework of choice. It uses Jekyll, the blog aware static site generator that powers  Github Pages.

This write up details the process of getting setup and any gotchas I encountered for my own future reference and for anyone that might find this useful.

The setup detailed in this writeup was carried out on my Mac Book Pro, running OS X Mavericks and a zsh terminal.

##Prerequisite:

1. Ensure you have [git](http://git-scm.com/) installed. If you have [Xcode tools](https://developer.apple.com/xcode/downloads/) then you should already have git available on your machine.
2. Install [rvm](https://github.com/wayneeseguin/rvm) or [rbenv](https://github.com/sstephenson/rbenv) with ruby version 1.9.3. Despite Octopress docs suggesting ruby versions greater than 1.9.3 would suffice, I had issues trying to use v2.0 as some of the Octopress dependencies didnt seem to support it.
3. Install [Bundler](http://bundler.io/),  the Ruby dependency manager.

##Setup:

Obtain Octopress by cloning it onto your local machine and navigate into the cloned folder.

In my instance I cloned it into a directory called "blog" as follows:

```
$ git clone git://github.com/imathis/octopress.git blog
cd blog

```
Install all the required dependencies:

```
$ bundle install

```
Install the default Octopress theme:

```
$ rake install

```

#Deployment

For easy publishing and to get free hosting for my blog I decided to use [Github pages](https://pages.github.com/) which also provides me with the domain `http://farai.github.io`.

To get the hosting setup, log into your [Github](https://github.com/) account and [create a github repository](https://github.com/repositories/new) with a name in the format of `username.github.io` where username is your Github user name. Ensure the name of your repository is in the correct format so that Github pages will be able to locate and serve your site as it will serve everything from the master branch of this repo like the web root directory on a server.

As the generated content will be served from the master branch of your repo you will want to work off a separate branch when making changes to your repo. Octopress provides a rake task that helps you setup a good work flow so you can easily manage and deploy:

```
$ rake setup_github_pages

```
You will notice after running the `setup_github_pages` task a new branch will have been created for you called "source" and a folder named "_deploy". When making changes to your blog you will now be working off the source branch and every time you perform a deployment, the changes you've made will be copied into the _deploy folder then pushed upto into the master branch by another set of deployment tasks.

To perform a deployment run the tasks:
```
$ rake generate
$ rake deploy

```

At this stage your site should now be deployed. The pending task would be to ensure you save site changes under source control by committing your changes on the "source" branch as follows:

```
$ git add .
$ git commit -m 'your desired commit message'
$ git push origin source

```
Remember to always commit changes made on your source branch.

If you now go ahead and visit `http://yourgithubusername.github.io` you should now be able to see your live site.

#Custom Theme

Upon completion of the setup, I didn't quite like the default Octopress theme and if you share the same feeling, the following process details how I added a custom theme.

I settled on the [Octoflat](http://github.com/alexgaribay/octoflat) theme by Alex Garibay and you can choose from a variety of other nice [3rd party Octopress themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes).

To install the custom theme I ran the following commands:

```
$ cd blog
$ git clone https://github.com/alexgaribay/octoflat .themes/octoflat
$ rake "install[octoflat]"
$ rake generate
$ rake deploy

```
Note that I quoted the arguments to rake on the install command as opposed to running `rake install['octoflat']` as most instructions suggest. This was intentional and due to the fact that instructions found in the docs are Bash oriented and I'm using a Zsh terminal which had me getting the error `zsh: no matches found: install[octoflat]`.

#Creating my first post

Octopress also provides a task to help you create your posts preloaded with metadata and according to Jekyll's naming conventions.

Creating my first post was as easy as running:

```
rake "new_post[Setup Octopress blog with Github Pages]"

```
And thats all that was to setting up my new Octopress blog.
