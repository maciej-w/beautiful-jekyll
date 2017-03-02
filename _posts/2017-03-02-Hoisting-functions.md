---
layout: post
title: Function hoisting
subtitle: how function declaration and expressions are called
bigimg: ../img/analog.jpg
---

### One of the thinks which I learned recently is how function declaration and function expression are hoisted. I wrote this post to not forget. Enjoy and sorry for potential errors!

As a quick reminder

** Function Declaration:
{% highlight javascript %}
function declaration () {
  return "function declaration!"
}
{% endhighlight %}

** Function Expression:
//anonymous function expression
{% highlight javascript %}
var expression = function () {
  return "anonymous function expression!"
}

//named function expression
{% highlight javascript %}
var expression = function expression () {
  return "named function expression!"
}

{% endhighlight %}

What gets returned in this case?

{% highlight javascript %}
function testMe(){
    function test() {
        return 3;
    }
    return test();
    function test() {
        return 8;
    }
}
alert(testMe());
{% endhighlight %} 

If you said 8 congratulations! If not, I'll try to quickly explain why it's not the case.

The behaviour above is caused by hoisting. What that means is that before the code is 'run', all variables and apparently function
declarations are hoisted to the top of our code. So this code during runtime would look like this:

{% highlight javascript %}
function testMe(){
    function test() {
        return 3;
    }
    // test() -> 3
    function test() {
        return 8;
    }
    // test() -> 8
    return test();    
}
alert(testMe());
{% endhighlight %} 

So the way it works, and testMe() is able to reach 8 is because before the return statements is reached the second statement
which returns 8 is 'lifted' above the return statement and overwrites the first one which returns 3. It's the same as in this case:

{% highlight javascript %}
var a = 1;
var a = 3;

console.log(a) // -> 3;
{% endhighlight %} 

What about Function Expression?

{% highlight javascript %}
function testMe(){
    var test = function() {
        return 3;
    };
    return test();
    var test = function() {
        return 8;
    };
}
alert(testMe());
{% endhighlight %} 

The result here is 3. Why? As mentioned before variables are hoisted, and here we've got variables, don't we?

Let's have a look how all get's sorted by the javascript engine before testMe() get's called.
{% highlight javascript %}
function testMe(){
    var test = undefined;
    var test = undefined;
    //we assign a value to test
    test = function() {
        return 3;
    };
    //we return the value 3
    return test();
    //this is the end, we don't reach value 8
    var test = function() {
        return 8;
    };
}
alert(testMe());
{% endhighlight %} 

In this case two variables got hoisted to the top of the scope, then a function has been assigned to it and we returned that value. 

The article which motivated me to write my own to better remember 'this' hoisting stuff is here: https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/
