---
layout: post
title: Dependency Injection
subtitle: DI in Angular2
bigimg: ../img/analog.jpg
---

### What is and how to use Dependency Injection (DI)

DI is a build in feature in Angular. It allows you injecting services directly into your modules. 

Let's have a look at the following code - without DI:

{% highlight javascript %}
export class Car {
 
  public engine: Engine;
  public tires: Tires;
  public description = 'No DI';
 
  constructor() {
    this.engine = new Engine();
  }
 
  // Method using the engine and tires
  drive() {
    return `${this.description} car with ` +
      `${this.engine.cylinders} cylinders and ${this.tires.make} tires.`;
  }
}
{% endhighlight %} 
source: https://angular.io/guide/dependency-injection#why-dependency-injection

In the above example we create a new class and in the constructor we initialize an Engine. Nothing special. The reason which
helped me to understand the need of DI is what happens if we have to add a new parameter to the Engine class in the future, e.g. number of cylinders?
It'll break the class. The above Car class in not flexible and when writing our code we want to make the job easy for us and for devs who work when we leave.

How can we fix the above?

First of all we can create an engine service:

{% highlight javascript %}
import { Injectable } from '@angular/core';

// The below @Injectable() decorator tells Angular that we want our service to be available for DI
// Google advises using it on every Service
@Injectable()
export class Engine {
  cylinders: any;

  setEngine(newCylinders) {
    this.cylinders = newCylinders;
  }

  getEngine(): any {
    return this.cylinders;
  }
}

{% endhighlight %} 

So we've got our Service, now we need to tell Angular that we want to inject it into a Module. There are two ways of achieving that:
1) we make it available to the whole app
2) we make it available to a selected Component

The first might be useful in the so called Singleton (might be a database Connection). We'll pick the second one. I go to my my-car.module.ts:

{% highlight javascript %}
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

// imported here
import { Engine } from '../services/engine.service';

@NgModule({
  imports: [
    CommonModule
  ],
  providers: [
    Engine // <-- added Dependancy
  ],
  declarations: []
})
export class UserDemoModule { }

{% endhighlight %} 

Now I can use my Engine service in the my-car.component.ts

{% highlight javascript %}
import { Component, OnInit } from '@angular/core';

import { UserService } from '../services/engine.service';

@Component({
  selector: 'app-my-car',
  templateUrl: './my-car.component.html',
  styleUrls: ['./my-car.component.css']
})
export class Car {
 
  public tires: Tires;
 
  // Angular will inject `Engine` here.
  // We set it as a `private` property.
  constructor(private engine: Engine) {
  }
 
}

{% endhighlight %} 

And as you see the class above has the Engine injected and whenever we change the Engine Service we do not have to be afraid that our class 
will break.

We can as well use methods from our Service this way:

{% highlight javascript %}
  this.Engine.setEngine(12);
{% endhighlight %} 
