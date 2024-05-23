---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
zoom: 100%

style: |
  .small-text {
    font-size: 0.45rem;
  }
  .smaller-text {
    font-size: 0.8rem;
  }
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---


# Design Patterns 
## (and their use in Java)

![bg left:40% 80%](https://lampobike.com/uploads/allimg/20200703/1-200F3110155a7.jpg)


---
# Agenda
- Very speedy & short theory intro
- Demo of app
- App's code walkthrough 
- Questions 

* <p class="small-text">That I may or may not know the answers to 😅</p>
![bg left:55% 80](https://d3j2bju5c7tc02.cloudfront.net/2017_39/cropped-636420530221108518IMG36413.jpg)

---
# What?
* Solutions to commonly occurring problems in software design.
* They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.
* My approach for this project was practical
    * but bad


---
# 3 types of patterns
* **Creational** - provide object creation mechanisms that increase flexibility and reuse of existing code <!--creational these provide object creation mechanism that increase flexibility and reuse of exisitng code -->
* **Structural** - <!-- Structural - These explain how to assemble objects and classes into larger structures, while keeping these structures flexible and efficient.--> how to assemble objects and classes into larger structures, while keeping these structures flexible and efficient
* **Behavioral** - effective communication and the assignment of responsibilities between objects <!--Behavioral patterns take care of effective communication and the assignment of responsibilities between objects.-->
---
Patterns we'll see:
<!--I am going to highlight the ones I've used in the project:-->
* **Singleton pattern** (Logger)
* **Chain of Responsibility** (coin changer)
* **Strategy pattern** (Payment)
* **Dependency injection** (Spring Beans)
* **DAO** (DrinkService)
* **Method factory**
* Honorable mentions: 
    * <p class="smaller-text">Encapsulation (OOP,   getters/setters)</p>
    * <p class="smaller-text">Guard clauses (Payment status...)</p>
    * <p class="smaller-text">Repository pattern (Spring's built-in CrudRepository)</p>

---
# Singleton
![bg right:55% 60%](https://s3.ap-southeast-1.amazonaws.com/saleor.lizard/products/singleton-glen-ord-12-years_654c1052.png)
* Creational
* Only one instance <!--only one instance of an object -->

* Advantages:
    * Access from anywhere within the program
    * Thread safe by default

---
# Singleton
- Disadvantages:
    * Tight coupling
    * Introduces Global state
        <!--* Global state Which might make debugging or changing the object hard in the long run-->
    * In Spring Boot because of DI you should probably use Beans and their Bean Scope (notably `singleton`, `application` scopes)
    <!-- * In Spring Boot because of availability of dependency injection you should probably just use Beans and their Bean Scope (notably `singleton`, `application` scopes)-->

--- 
# Singleton
* Example usage:
    * Connection pool for DB access
    * Logging service (for the whole application) 
---

# Chain of Responsibility
![bg right:50% 100%](https://refactoring.guru/images/patterns/diagrams/chain-of-responsibility/solution1-en.png?id=dccad3e628bd2b8f1856c99369ca6e5b)
* Behavioral pattern
* Pass requests along chain of handlers
* Either process, or process & pass, or leave alone and only pass to the next handler

---
# Chain of Responsibility
* Example usage:
    * Authentication middleware
    * Servlet filters (pre & post processing of a request)
--- 
# Chain of Responsibility
* Advantages:
    * Loose coupling between objects
* Disadvantages:
    *   it can result in a lot of implementation classes
    *   & maintenance is harder if most of the code is shared among them (duplicated code)
    * if processor fails to call next one -> the request is dropped

---
# Strategy
![bg left:50% 100%](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/StrategyPattern_IBrakeBehavior.svg/1920px-StrategyPattern_IBrakeBehavior.svg.png)
* Behavioral 
* Define a family of algorithms, put each to seperate class, make their objects interchangable
    * My code fails at that (we will see that later :smile:)
<!-- The clients that use the "break()" call can use it interchangibly at runtime, they do not care if they break with ABS or just brake normally, to them it doesn't matter-->


--- 
# Dependency injection
* All data that functions or classes need must be passed to them.
<!-- This approach creates a separation between components and dependencies. -->
* Advantages:
    * Loose coupling
    * Testability (unit tests)
    * Flexible <!-- Flexible as in - flexible dependency managment, different depdencnesi can be injected -->
    * Maintenance
---
# Dependency injection
* Disadvantages 
    * Code complexity
    * Overhead
    * Runtime errors <!-- Runtime errors instead of compile time-->

---
# DAO Pattern
* Structural pattern
* Data Access Object
* Isolate business layer from persistance layer (DB etc.) through abstract API
<!--The API hides from the application all the complexity of performing CRUD operations in the underlying storage mechanism. -->


--- 
# Factory Method Pattern
* Creational 
* Deal with the problem of creating objects without having to specify their exact class. 
* Advantages
    * Modular expandability of the application
        <!-- separating the creation of payment strategies from the rest of the application in my case -->
    * Good testability
* Disadvantages 
    * More abstraction
    * Object creation is not as transparent anymore
        <!-- Aka have to check the implementation of the factory method otherwise i dunno what is being created -->
---

# Encapsulation 
![bg right:50% 100%](https://www.simplilearn.com/ice9/free_resources_article_thumb/Encapsulation_in_Java.png)
- Getters & setters for `private` members

---

# Stop!
## ~~Hammer~~ Demo time!
⌛

---
# A Vending Machine!
(or as the folder is called - "coke dispenser" :smile:)
* Caveats: 
    * Unlimited <!--machine has unlimited coins and types of coins --> coins
    * Paying by card is not implemented
    * No way for company to manage available drinks


---
# Sources
* https://refactoring.guru/
* https://www.baeldung.com/
