---
layout: post
title: Floating Divs and fixing stuff
subtitle: Float
bigimg: ../img/analog.jpg
---

### How to fix a layout which contains divs containing only floated elements

Suppose you've got 2 divs, one containing floating divs and one with a border

{% highlight html %}
 <div>
    <div class="box"><span>1</span></div>
    <div class="box"><span>2</span></div>
    <div class="box"><span>3</span></div>
    <div class="box"><span>4</span></div>
    <div class="box clear"><span>5</span></div>
  </div> 
  <div class="floatContainer">
    <div class="box"><span>1</span></div>
    <div class="box"><span>2</span></div>
    <div class="box"><span>3</span></div>
    <div class="box"><span>4</span></div>
    <div class="box"><span>5</span></div>
  </div> 
{% endhighlight %} 

But look it's broken!

<script async src="//jsfiddle.net/alexwas/x049de9L/embed/"></script>

Fix is pretty easy. We create an empty div and apply a clear:both style to it and place the div between the previous two divs.

{% highlight html %}
<div style="clear:both"></div>
{% endhighlight %} 

<script async src="jsfiddle.net/alexwas/95m3fe2g/2/"></script>

And that's it!
