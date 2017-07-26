---
layout: post
title: Playing with Arrays - part II
subtitle: filter function
bigimg: ../img/analog.jpg
---

### The filter function lets you quickly filter data from an array without using a forEach or for loop.

We'll use the same object as before.

{% highlight javascript %}
var symbols = getHighPrices([
  {symbol:"GG", price:500.65},
  {symbol:"AA", price:1085.20},
  {symbol:"BB", price:135.00}
]);
{% endhighlight %} 

The great thing about filter function is that you can quickly filter your array without using forEach or a standard for loop.

Let's have a look on how to return stocks with prices higher than 450.00, it's easy:

{% highlight javascript %}
function getHighPrices(stocks){  
  return stocks.filter(
    //The below is the predicate function 
    function(stock){
      return stock.price >= 400;
  })
};
{% endhighlight %} 

The main part of the above is a predicate function, a function which returns True or False based on a condition, in this case the
condition is 'stock.price >= 400'. If the result is True, the filter function pushes the 'current' stock element (e.g. {symbol:"GG", price:500.65})
to an array. This Array is then returned by using:

{% highlight javascript %}
return stocks.filter(...
{% endhighlight %} 

This way we can quickly filter arrays. In the next post I'll show you how to chain map and filter! 
