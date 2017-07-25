---
layout: post
title: Playing with Arrays - part I
subtitle: map function
bigimg: ../img/analog.jpg
---

### The map function might take you to the next level. Is pretty easy to use and works with Async code.

It might be slower then a classical for loop, but if you are planning on using Observables and playing with async arrays it's the only option.

Let's suppose we've got the following array of objects:

{% highlight javascript %}
var symbols = getSymbols([
  {symbol:"GG", price:500.65},
  {symbol:"AA", price:1085.20},
  {symbol:"BB", price:135.00}
]);
{% endhighlight %} 

You can loop through the code above using the standard for loop and returns the symbol this way:

{% highlight javascript %}
function getSymbols(stocks){  
  var arr = [];  
  for (var i = 0; i <= stocks.length; i++) {
       arr.push(stocks[i].symbol);
    }
  return arr;
};
{% endhighlight %} 

Or you can use the build in map method this way:

{% highlight javascript %}
function getSymbols(stocks){
  return stocks.map(function(stock){
    return stock.symbol;
  })
};
{% endhighlight %} 

What it does it accepts a closure to which each element of the array is passed. Have a look below:

{% highlight javascript %}
/*
* Each element of the array is passed through this closure function.
* 'stock' is that single array element
*/
function(stock){
    return stock.symbol;
// The stock.symbol is being added to an 'invisible' array. We don't see it but it gets created behind.
}
{% endhighlight %} 

In this case we don't have to take care of a for loop, we don't need to create new variables. We just pass our array through the map() function.

If you want to check the performance have a look here:
https://jsperf.com/map-vs-for-loop-performance/6
