---
layout: post
title: Playing with Arrays - episode I
subtitle: map function
bigimg: ../img/analog.jpg
---

### This function might take you to the next level. Is pretty easy to use and works with Async code.

It might be slower then a classical for loop, but if you are planning on using Observables and playing with async arrays it's the only option.

{% highlight javascript %}
var symbols = getSymbols([
  {symbol:"GG", price:500.65},
  {symbol:"AA", price:1085.20},
  {symbol:"BB", price:135.00}
]);
{% endhighlight %} 

You can loop through the code above using the standard for loop and return the symbols like this:

{% highlight javascript %}
function getSymbols(stocks){  
  var arr = [];  
  for (var i = 0; i <= stocks.length; i++) {
       arr.push(stocks[i].symbol);
    }
  return arr;
};
{% endhighlight %} 

Or you can use build in map method:

{% highlight javascript %}
function getSymbols(stocks){
  return stocks.map(function(stock){
    return stock.symbol;
  })
};
{% endhighlight %} 

Does the same as for loop and it's shorter. What it does it accepts a closure to which each element of the array is passed like below:

{% highlight javascript %}
//Each element of the array is passed through this function
//'stock' is that single array element
function(stock){
    return stock.symbol;
// adds the stock.symbol to an 'invisible' array
}
{% endhighlight %} 
