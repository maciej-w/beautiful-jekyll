---
layout: post
title: How to toggle elements on click in Angular 2
subtitle: Enothing exciting
bigimg: /img/path.jpg
---

###Sometimes we want to have a possibility of applying a class to an HTML element after clicking it. This, thanks to the (click) element of Angular 2, makes the whole process really straightforward.

Suppose you're using Bootstrap 3 this is how your element should look like:

{% highlight javascript %}
<a class="btn btn-app"
   (click)="isSelected = !isSelected"
   [ngClass]="{'button-selected': isSelected}"
   id="actionType1">
   <i class="fa fa-envelope-o"></i> Email
</a>
{% endhighlight %} 

The follwoing bit of code is an input, because it is enclosed in () and it handles clicks. 
(click)="isSelected = !isSelected"

On a click it grabs iSelected variable and change it from true to false. But wait a minute, where is isSelected? Obviously we need to create it in the class component. I use Typescript so in my case it will look like this because I want it to be set to false, so the class which adds a green border doesn't appear until the object is clicked.

export class AddActionComponent {

  //is button clicked to change class - create a new component anc choke tickets there then page 100!
  public isSelected: boolean = false;

}
