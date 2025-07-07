src = https://www.youtube.com/watch?v=kF7rQmSRlq0

# The Acronym

- Single responsibility
- Open/closed
- Liskov substitution
- Interface segregation
- Dependency inversion

# Single responsibility principle

Each class should have a single responsibility.  

Giving a class multiple responsibilities equals **more chances to introduce bugs** when you modify your class.  

Besides, having one class per functionality makes **team work easier** by allowing each developer to work on a specific file.  
Meaning **less merge conflicts** when the work is done and all devs push their code to the repository.  

Separating responsibilities has the added benefit of letting us **reuse** functionality **without** having to **repeat** the code in several places.  

Be careful not to take this principle too far.  
Single responsiblity doesn't mean your class should only do one thing.  
It just means that everything it does should be very closely related, so you don't end up with bloated classes.  

# Open/closed principle

Our code should be open to extension but closed to modification.  
If we need to add some functionality to our application, then we shouldn't be editing the existing classes.  

After all, we spent ages writing unit tests for all of those methods, and we don't want them to break...  
On top of that, adding new functionality to existing classes may have unexpected consequences.  

So, how to implement additional functionality without changing the existing methods or classes?  
One way to achieve this is to use the **Decorator pattern**.  

## Decorator Pattern

https://www.perplexity.ai/search/explain-the-decorator-pattern-p7UVZ6T3TTKZ4XME0fSzPw  

New functionalities are added by creating decorators, leaving existing classes **untouched**.  

Instead of modifying the code, we create a new class that implements the same interface as the existing class.  
We can then declare our method without affecting the other code in our application.  

The benefit of this approach is that you can use **dependency injection** at runtime to be able to control when the new class is used.  

**However**, we can only use this approach if the method we want to extend is both public and included in the interface.  

Basic example:
```ts
// Base component  
interface Coffee { cost(): number; }  
class BasicCoffee implements Coffee { cost() { return 2; } }  

// Decorators  
class MilkDecorator implements Coffee {  
  constructor(private coffee: Coffee) {}  
  cost() { return this.coffee.cost() + 0.5; }  
}  

class SugarDecorator implements Coffee {  
  constructor(private coffee: Coffee) {}  
  cost() { return this.coffee.cost() + 0.2; }  
}  

// Usage: Extend functionality without modifying BasicCoffee  
const coffee = new SugarDecorator(new MilkDecorator(new BasicCoffee()));  
console.log(coffee.cost()); // Output: 2.7  
```
Here, BasicCoffee remains closed to modification, while decorators extend its behavior.

## Extension Methods

Another great option is to use Extension Methods.  
An extension method allows us to add a method to an existing class without actually having to change the file where our class is defined.    

Provided that you have the **namespace** for your extension **imported**, you can then use the method in the same way you would do if that method was part of the original class.  

The only **downside** of using extension methods is that, unlike the decorator pattern, you cannot switch at runtime which method is used.  

# Liskov substitution principle

A child class should be able to do everything that the parent class can.  

# Interface segregation principle

Interfaces provide a contract that your classes need to implement.  
If you have particularly bulky interfaces, then you classes have to implement methods they might not end up using.  

To overcome this, you can split the methods into different interfaces.  
For example, one interface for writing, one for reading, and one for deleting.  

When you do need to use of all of the different methods, you can always create a main interface that inherits from all the others.  

This way, you only need to implement the methods you're actually going to use.  

# Dependency inversion principle

The Dependency Inversion Principle ensures that both high-level and low-level components depend on shared **abstractions**, not on each other directly.   
This inversion of traditional dependency direction leads to more modular, maintainable, and adaptable software systems.

## How to Apply DIP? 

- Program to **interfaces**, not implementations.
- Use **dependency injection** to supply dependencies from the outside, rather than instantiating them directly inside classes
- Avoid direct references to concrete classes in high-level modules

# What is dependency injection? And why should I use it?

Dependencies, in the context of dependency injection, are  objects a specific class depends on.  
For example, a computer needs RAM, a CPU, an SSD, and a GPU. These components are the computer's dependencies.  

If we think of this computer as a class in OOP, we could either create the components in the Computer class, or we could create them somewhere else.  
If we create them in the class (as attributes), every computer (every instance of the Computer class) will have the same specs.  

## Constructor injection

One way of injecting dependencies is via **Constructor injection**.  
We pass the computer's components as constructor arguments, which allows us to give each computer instance different components.  

## Libraries (complex injection)

Besides constructor injection, there are more complex dependency injection **libraries** that inject the dependencies behind the scenes.  

With these libraries, we can usually also decide about the lifetime of our dependencies.  

In our Computer class example, there is no reason for the GPU to be active when we just want to do some office work, we could save some resources.  
But for playing video games, we need the GPU.  

TO BE CONTINUED

## Dependency injection is a design pattern

Instead of initializing an object in a method, we pass it as an argument, or we get the object from somewhere else.  
That way, the place where you create the object is different from the place where you use it.  

## The Benefits

This separation is useful for **testing**, and it makes your code more **maintainable**, and  more **flexible**.  

