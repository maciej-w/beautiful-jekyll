---
layout: post
title: *ngSwitch
subtitle: Angular 2 build in directives
bigimg: ../img/analog.jpg
---

### You can use \*ngSwitch when you're planning on displaying something based on a condition.

Let's consider the following:

{% highlight html %}
<div class="container">
  <p *ngIf="var == 1">1</p>
  <p *ngIf="var == 2">2</p>  
  <p *ngIf="var == 3">3</p>  
  <p *ngIf="var != 1 && var != 2 && var != 3">Default</p>  
</div>
{% endhighlight %} 

What if you have to add another possibility now, a var = 4? You'd have to add another line and update the Default condition value.

In this case the \*ngSwitch is the best option:

{% highlight html %}
<div class="container" \[ngSwitch]="var">
  <p \*ngSwitchCase="1">1</p>
  <p \*ngSwitchCase="2">2</p>  
  <p \*ngSwitchCase="3">3</p>  
  <p \*ngSwitchDefault>Default</p>  
</div>
{% endhighlight %} 

As you can see we pass the variable to ngSwitch in the div container, so ngSwitchCase has got access to the value. The Default option is pretty 'safe' as well if we forget to add a condition as well.
