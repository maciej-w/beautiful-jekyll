---
layout: post
title: Queryselector() in functions
subtitle: passing parameters to queryselector()
bigimg: ../img/analog.jpg
---

### If you have to access an html element which has got additional attributes use queryselector, that's the thing now!

Suppose this is your HTML area and you want to remove an element if a condition is met:

{% highlight html %}
<ul class="ulClass">
  <li class="arrow" actionindex="0"></li>
  <li class="arrow" actionindex="1"></li>
  <li class="arrow" actionindex="2"></li>
  <li class="arrow" actionindex="3"></li>  
</ul> 
{% endhighlight %} 

The quickest and "modern" way to locate it in the DOM is to use queryselector(), in this case we grab index 1:

{% highlight javascript %}
document.querySelector("li[actionindex='1'][class='Arrow']")
{% endhighlight %} 

But what if we want to programmatically remove an index if a condition is met but you build lists like this on other pages? 
The solution would be to locate the parent <ul> first by using the old getElementById - don't see the reason why not in this case - and then you
could use queryselector to locate the children and the index in question. Have a look below:

{% highlight javascript %}
function removeIdx(idx){	
	
	var x = document.getElementById("ulClass");
	x.querySelector("li[actionindex='"+ idx +"'][class='arrow']").style.display = "none";
}		
{% endhighlight %} 

Because our actionindex places the value in "" we need to place the whole expression in single quotes.

