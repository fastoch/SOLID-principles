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

### What is Dependency Injection?



## Extension Methods

Another great option is to use Extension Methods.


# Liskov substitution principle


