---
layout: post
title:  "Setting up Angular 2 project"
date:   2016-11-30 20:45:57 +0000
categories: Javascript Angular mDesign Infinity
---

### How to set up an Angular 2 project with Typescript in < 10 minutes.

Angular 2 is greatly designed to co-operate with [typescript] and [nativescript]. I won't focus on nativescript, but briefly it has 
great support if you want to develop for mobile using Angular 2. 

Typescript is being used to write Javascript (after processing) but it has got support for types, classes and more.

**Back to our Angular 2 set up:**

First you'll need Node.js installed - depending on what system you're using (Windows, Linux or Mac) there are different steps - please follow [nodejs].

After you've got that set up open your Terminal or Command Line and run:

{% highlight shell %}
npm install -g typescript 
{% endhighlight %} 


Angular provides a command line utility tool called Angular CLI - it's great, it lets you add components and all their dependencies (to ng-module for example) automatically. To install it just type:

{% highlight shell %}
npm install -g angular-cli@1.0.0-beta.18
{% endhighlight %} 


After a long install, if using Linux or Mac, you might get an error regarding watchman - it is used to observe changes in your files and restarting the server running your app - something like nodeman for node.js apps. To install it just run:

{% highlight shell %}
brew install watchman
{% endhighlight %} 


As you can see this time we're using brew for installation (previously npm). If you haven't got homebrew installed run:

{% highlight shell %}
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" 
{% endhighlight %} 


And finally everything is ready!

We've got:
- Node.js
- npm (part of node)
- typescript
- watchman
- homebrew

### Now we can finally build our first Angular 2 project using Angular CLI.

Enter your project or documents directory and run:

{% highlight shell %}
ng new hello-world-angular2
{% endhighlight %} 

This will get your project build and configured, next enter the hello-world-angular2 directory.

{% highlight shell %}
cd hello-world-angular2
{% endhighlight %} 

You can review your app directory using:

- tree -F comnmand - it'll show you what's been created

And finally we're ready to run our app! Run the following in the app directory:

{% highlight shell %}
ng serve
{% endhighlight %} 

Ta da! In the browser open http://localhost:4200

Your're app is up and running!

[typescript]: https://www.typescriptlang.org/
[nativescript]: https://www.nativescript.org/
[nodejs]: https://nodejs.org/en/
