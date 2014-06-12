---
layout: post
title: "Client Side Dependency Management with Bower"
date: 2014-06-12 19:25:26 +0100
comments: true
categories:
---
As part of a conquest to improve my general front-end skills, I decided to address the issue of dependency management
and decided to familiarise myself with [Bower](http://bower.io/).

Bower is a dependency management solution that helps you overcome the stress of front-end dependency management. It will help you
manage your web assets like Javascript, HTML and CSS.

In greater detail and as defined by the Bower team:
> Bower is a package manager for the web. It offers a generic, unopinionated solution to the problem
> of front-end package management, while exposing the package dependency model via an API that can be consumed by a more opinionated build stack.
> There are no system wide dependencies, no dependencies are shared between different apps, and the dependency tree is flat.

In this post I detail the installation process, issues encountered, how to use it and anything else I found worth remembering.

##Getting Started...

Bower has a few dependencies of its own that need to be satisfied before you can use it. To get started ensure you have installed the following:

1. [Node.js](http://nodejs.org/)
2. Npm - comes bundled with Node.js installation
3. [Git](http://git-scm.com/)

##Installation

Install Bower globally using npm with ```-g``` flag by running the following:

```
$ npm install -g bower

```
My first attempt of running the above command failed with the following error:

```
npm ERR! Error: EACCES, mkdir '/usr/local/lib/node_modules/bower'
npm ERR!  { [Error: EACCES, mkdir '/usr/local/lib/node_modules/bower']
npm ERR!   errno: 3,
npm ERR!   code: 'EACCES',
npm ERR!   path: '/usr/local/lib/node_modules/bower',
npm ERR!   fstream_type: 'Directory',
npm ERR!   fstream_path: '/usr/local/lib/node_modules/bower',
npm ERR!   fstream_class: 'DirWriter',
npm ERR!   fstream_stack:
npm ERR!    [ '/usr/local/lib/node_modules/npm/node_modules/fstream/lib/dir-writer.js:36:23',
npm ERR!      '/usr/local/lib/node_modules/npm/node_modules/mkdirp/index.js:37:53',
npm ERR!      'Object.oncomplete (fs.js:107:15)' ] }
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

```

From looking at the error I could tell this was the result of a permissions issue. I attempted to resolve by running the install
command as sudo to no avail. If like me, you run into the same issue; you can resolve by changing the ownership of the
**/usr/local** directory to your $USER as follows:

```
$ sudo chown -R $USER /usr/local

```

After running the above; if you re-run the install command, it should now succeed with no problem. You can now verify that bower has successfully
installed by running the following command in your terminal which should then return usage instructions:

```
$ bower

```

##Lets Start Using Bower


###Searching For Packages

Locating packages can be done in two ways. You can either find available packages using the [component directory](http://bower.io/search/) or searching using bower's
command line ```search``` feature.

For example to search for the popular [bootstrap](http://getbootstrap.com/) front-end framework, you can simply formulate your command line query like so:

```
$ bower search bootstrap

```

The query will return a large result set in the format **<package_name><git_end_point>**. You can use the package name or the git endpoint to install the package.

```
Search results:

    bootstrap git://github.com/twbs/bootstrap.git
    angular-bootstrap git://github.com/angular-ui/bootstrap-bower.git
    sass-bootstrap git://github.com/jlong/sass-bootstrap.git
    bootstrap-sass git://github.com/jlong/sass-twitter-bootstrap

```

###Installing Packages via Command Line

Having chosen a package to install, you can use the ```install``` command with the name of the package you wish to install as the argument.

```  
$ bower install <package>

```

You can also choose to install a specific version of a package by using the hash symbol between the package name and the required version number.

```  
$ bower install <package_name>#<version_number>

```

###Installing Packages Using bower.json file

Using the bower.json to install packages provides advantages such as eliminating the need to commit your applications dependencies to version control since
all the info will be in the file and will allow you and other project collaborators to easily reproduce an identical software stack.

You can create the file in your application root directory or run ```bower init``` command which will generate a template file for you to list your dependencies.

The example below shows a bower.json file which defines some information on the project and a list of its dependencies.

```
{
  "name": "sample-app",
  "version": "0.0.1",
  "dependencies": {
    "sass-bootstrap": "~3.0.0",
    "jasmine": "~2.0"
  }
}
```

Once you have defined all you project dependencies, you can install them all at once by executing the ```bower install``` command.

##Other useful commands

```
$ bower update

```
Will update all your dependencies specified in your bower.json file while abiding by the version restrictions you've specified.

```
$ bower update <package_name>

```
Will update the specified package name

```
$ bower uninstall <package_name>

```  
Will uninstall the specified package
