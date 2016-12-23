---
layout: post
title: How to toggle a CSS class on click in Angular 2
subtitle: Exciting stuff
bigimg: ../img/analog.jpg
---

### Sometimes we want to have a possibility of applying a class to an HTML element after clicking it. This, thanks to the (click) element of Angular 2, makes the whole process pretty straightforward.

Suppose you're using Bootstrap 3 this is how your element could look like:

{% highlight html %}
<a class="btn btn-app"
   (click)="isSelected = !isSelected"
   [ngClass]="{'button-selected': isSelected}"
   id="actionType1">
   <i class="fa fa-envelope-o"></i> Email
</a>
{% endhighlight %} 

The following bit of code is an output, because it is enclosed in () and it handles events flow out of the component. In this particular example it's a click, but it can handle our own events set up in the component class.

{% highlight html %}
(click)="isSelected = !isSelected"
{% endhighlight %} 

On a click it grabs iSelected variable and change it from false to true and back. But wait a minute, where is isSelected? Obviously we need to create a variable handling a boolean in the class component. I use Typescript so in my case it will look like this. 

{% highlight javascript %}
export class AddActionComponent {

  //is button clicked is a boolean
  public isSelected: boolean = false;
}
{% endhighlight %} 

I want it to be set to false, so the class which adds a green border doesn't appear until the object is clicked (is equal true).

The following bit:

{% highlight html %}
[ngClass]="{'button-selected': isSelected}"
{% endhighlight %} 

Like you might have guessed [ngClass] is responsible for changing an element class based on a condition in this example. This how it works: button-selected is the name of the class and we want to apply it when isSelected is true. That's why I've set up isSelected=false at the beginning.

**button-selected must be wrapped in single quotes as it contains a -. In javascript you would have to use [] to use it, in Angular is single quotes**

As you can see using 2 angular elements we can apply different classes to object based on conditions. If you'd like to apply more that one condition to [ngClass] you could do it this way:

{% highlight html %}
[ngClass]="{'button-selected': isSelected, 'has-error':!myForm.controls['button'].valid}"
{% endhighlight %} 
