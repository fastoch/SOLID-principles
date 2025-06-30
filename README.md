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

Separating responsibilities has the added benefit of letting us reuse functionality without having to repeat the code in several places.  

Be careful not to take this principle too far.  
Single responsiblity doesn't mean your class should only do one job.  
It just means that everything it does should be very closely related, so you don't end up with bloated classes.  

# Open/closed principle

