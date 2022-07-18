![](Output.001.png)

**Evaluation Only. Created with Aspose.Words. Copyright 2003-2022 Aspose Pty Ltd.**

SOFTWARE DESIGN

PRINCIPLES

33  Software Design P rinciples / Features o f Good Design 

Features of Good Design

Before we proceed to the actual patterns, let’s discuss the process of designing software architecture: things to aim for and things you’d better avoid.

 Code reuse

Cost and time are two of the most valuable metrics when developing any software product. Less time in development means entering the market earlier than competitors. Lower development costs mean more money is left for marketing and a broader reach to potential customers.

**Code reuse** is one of the most common ways to reduce devel- opment costs. The intent is pretty obvious: instead of develop- ing something over and over from scratch, why don’t we reuse existing code in new projects?

The idea looks great on paper, but it turns out that making existing code work in a new context usually takes extra effort. Tight coupling between components, dependencies on con- crete classes instead of interfaces, hardcoded operations—all of this reduces flexibility of the code and makes it harder to reuse it.

Using design patterns is one way to increase flexibility of soft- ware components and make them easier to reuse. However,

34  Software Design P rinciples / Code reuse 

this sometimes comes at the price of making the components more complicated.

Here’s a piece of wisdom from Erich Gamma **1**, one of the founding fathers of design patterns, about the role of design

patterns in code reuse:

“

I see three levels of reuse.![](Output.002.png)

At the lowest level, you reuse classes: class libraries, contain- ers, maybe some class “teams” like container/iterator.

Frameworks are at the highest level. They really try to dis- till your design decisions. They identify the key abstractions for solving a problem, represent them by classes and define relationships between them. JUnit is a small framework, for example. It is the “Hello, world” of frameworks. It has Test ,

TestCase , TestSuite and relationships defined.

A framework is typically larger-grained than just a single class. Also, you hook into frameworks by subclassing somewhere. They use the so-called Hollywood principle of “don’t call us, we’ll call you.” The framework lets you define your custom behavior, and it will call you when it’s your turn to do some- thing. Same with JUnit, right? It calls you when it wants to exe- cute a test for you, but the rest happens in the framework.

There also is a middle level. This is where I see patterns. Design patterns are both smaller and more abstract than

\1. Erich Gamma on Flexibility and Reuse: **[https://refactoring.guru/ gamma-interview**](https://refactoring.guru/gamma-interview)**

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
35  ![](Output.003.png)Software Design P rinciples / Ext ensibility 

frameworks. They’re really a description about how a couple of classes![](Output.004.png) can relate to and interact with each other. The level of reuse increases when you move from classes to patterns and finally frameworks.

frameletWhatyouwisorkreusenicisedesignhigh-riskaboutideasthisandmiddleanda significantc onclayeptser isindependentlyinvthatestmentpatterns. Poattfocernsffon-er„ reuse in a way that is less risky than frameworks. Building a

crete code.

 Extensibility

**Change**is the only constant thing in a programmer’s life.

- You released a video game for Windows, but now people ask for a macOS version.
- You created a GUI framework with square buttons, but several months later round buttons become a trend.
- You designed a brilliant e-commerce website architecture, but just a month later customers ask for a feature that would let them accept phone orders.

Each software developer has dozens of similar stories. There are several reasons why this happens.

First, we understand the problem better once we start to solve it. Often by the time you finish the first version of an app,

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
36  ![](Output.005.png)Software Design P rinciples / Ext ensibility 

you’re ready to rewrite it from scratch because now you under- stand many aspects of the problem much better. You have also grown professionally, and your own code now looks like crap.

Something beyond your control has changed. This is why so many dev teams pivot from their original ideas into something new. Everyone who relied on Flash in an online application has been reworking or migrating their code as browser after browser drops support for Flash.

The third reason is that the goalposts move. Your client was delighted with the current version of the application, but now sees eleven “little” changes he’d like so it can do other things he never mentioned in the original planning sessions. These aren’t frivolous changes: your excellent first version has shown him that even more is possible.

There’s a bright side: if someone asks you to change something![](Output.006.png) in your app, that means someone still cares about it.

That’s why all seasoned developers try to provide for possible future changes when designing an application’s architecture.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
![](Output.005.png)

37 Design Principles 

Design Principles

What is good software design? How would you measure it? What practices would you need to follow to achieve it? How can you make your architecture flexible, stable and easy to understand?

These are the great questions; but, unfortunately, the answers are different depending on the type of application you’re build- ing. Nevertheless, there are several universal principles of software design that might help you answer these questions for your own project. Most of the design patterns listed in this book are based on these principles.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
38  ![](Output.005.png)Design Principles / Encapsulat e What Varies 

Encapsulate What Varies

Identify the aspects of your application that vary and separate them from what stays the![](Output.007.png) same.

The main goal of this principle is to minimize the effect caused by changes.

Imagine that your program is a ship, and changes are hideous mines that linger under water. Struck by the mine, the ship sinks.

Knowing this, you can divide the ship’s hull into independent compartments that can be safely sealed to limit damage to a single compartment. Now, if the ship hits a mine, the ship as a whole remains afloat.

In the same way, you can isolate the parts of the program that vary in independent modules, protecting the rest of the code from adverse effects. As a result, you spend less time getting the program back into working shape, implementing and test- ing the changes. The less time you spend making changes, the more time you have for implementing features.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
39  ![](Output.008.png)Design Principles / Encapsulat e What Varies 

Encapsulation on a method level

Say you’re making an e-commerce website. Somewhere in your code, there’s a getOrderTotal method that calculates a grand ![](Output.009.png)total for the order, including taxes.

We can anticipate that tax-related code might need to change

in the future. The tax rate depends on the country, state or even city where the customer resides, and the actual formu- la may change over time due to new laws or regulations. As a result, you’ll need to change the getOrderTotal method quite ![](Output.010.png)often. But even the method’s name suggests that it doesn’t care about *how* the tax is calculated.

1  method getOrderTotal(order) is
1  total = 0
1  foreach item in order.lineItems

4 total += item.price \* item.quantity

5 6 if (order.country == "US") 7 total += total \* 0.07 // US sales tax 8 else if (order.country == "EU"): 9 total += total \* 0.20 // European VAT 10

11 return total

*BEFORE: tax calculation code is mixed with the rest of the me thod’scode.*

You can extract the tax calculation logic into a separate method, hiding it from the original method.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
40  ![](Output.011.png)Design Principles / Encapsulat e What Varies 
1  method getOrderTotal(order) is
1  total = 0
1  foreach item in order.lineItems

4 total += item.price \* item.quantity

5

6 total += total \* getTaxRate(order.country) 7

8 return total 9

10 method getTaxRate(country) is 11 if (country == "US")

12 return 0.07 // US sales tax

13 else if (country == "EU")

14 return 0.20 // European VAT

15 else

16 return 0

*AFTER: you can get the tax rate b y calling a designated method.*

Tax-related changes become isolated inside a single method. Moreover, if the tax calculation logic becomes too complicat- ed, it’s now easier to move it to a separate class.

Encapsulation on a class level

Over time you might add more and more responsibilities to a method which used to do a simple thing. These added behav- iors often come with their own helper fields and methods that eventually blur the primary responsibility of the containing class. Extracting everything to a new class might make things much more clear and simple.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
41  ![](Output.012.png)Design Principles / Encapsulat e What Varies 

![](Output.013.png)

*BEFORE: calculating tax in* Order *class.![](Output.014.png)*

Objects of the Order class delegate all tax-related work to a special object that does just![](Output.015.png) that.

![](Output.016.png)

*AFTER: tax calculation is hidden from the* Order *class.![](Output.017.png)*

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
42  ![](Output.005.png)Design Principles / P rogram t o an Int erface, not an Implementation 

Program to an Interface, not an Implementation

Program to an interface, not an implementation. Depend on abstractions, not on concrete![](Output.007.png) classes.

You can tell that the design is flexible enough if you can easily extend it without breaking any existing code. Let’s make sure that this statement is correct by looking at another cat exam- ple. A Cat that can eat any food is more flexible than one that![](Output.018.png) can eat just sausages. You can still feed the first cat with sausages because they are a subset of “any food”; however, you can extend that cat’s menu with any other food.

When you want to make two classes collaborate, you can start by making one of them dependent on the other. Hell, I often start by doing that myself. However, there’s another, more flex- ible way to set up collaboration between objects:

1. Determine what exactly one object needs from the other: which methods does it execute?
1. Describe these methods in a new interface or abstract class.
1. Make the class that is a dependency implement this interface.
1. Now make the second class dependent on this interface rather than on the concrete class. You still can make it work with

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
43  ![](Output.019.png)Design Principles / P rogram t o an Int erface, not an Implementation 

objects of the original class, but the connection is now much more flexible.

![](Output.020.png)

*Before and after extracting the interface. The code on the right is more flexible than the code on the left, but it’s also more complicated.*

After making this change, you won’t probably feel any immedi- ate benefit. On the contrary, the code has become more com- plicated than it was before. However, if you feel that this might be a good extension point for some extra functionality, or that some other people who use your code might want to extend it here, then go for it.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
44  ![](Output.005.png)Design Principles / P rogram t o an Int erface, not an Implementation 

Example

Let’s look at another example which illustrates that working with objects through interfaces might be more beneficial than depending on their concrete classes. Imagine that you’re creat- ing a software development company simulator. You have dif- ferent classes that represent various employee types.

![](Output.021.png)

*BEFORE: all classes are tightlycoupled.*

In the beginning, the Company class is tightly coupled to con- ![](Output.022.png)crete classes of employees. However, despite the difference in their implementations, we can generalize various work-related

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
45  ![](Output.012.png)Design Principles / P rogram t o an Int erface, not an Implementation 

methods and then extract a common interface for all employ- ee classes.

After doing that, we can apply polymorphism inside the

Company class, treating various employee objects via the ![](Output.023.png)Employee interface.

![](Output.024.png)

*BETTER: polymorphism helped us simplify the code, but the rest of the* Company *class still depends on the concrete employee classes.![](Output.025.png)*

The Company class remains coupled to the employee classes. This![](Output.026.png) is bad because if we introduce new types of companies that work with other types of employees, we’ll need to over- ride most of the Company class instead of reusing that code.![](Output.027.png)

To solve this problem, we could declare the method for get- ting employees as *abstract*. Each concrete company will imple-

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
46  ![](Output.012.png)Design Principles / P rogram t o an Int erface, not an Implementation 

ment this method differently, creating only those employees that it needs.

![](Output.028.png)

*AFTER: the primary method of the* Company *class is independent from concrete ![](Output.029.png)employee classes. Employee objects are created in concrete   company subclasses.*

After this change, the Company class has become independent from![](Output.030.png) various employee classes. Now you can extend this class and introduce new types of companies and employees while still reusing a portion of the base company class. Extending the base company class doesn’t break any existing code that already relies on it.

By the way, you’ve just seen applying a design pattern in action! That was an example of the *Factory Method* pattern. Don’t worry: we’ll discuss it later in detail.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
47  ![](Output.031.png)Design Principles / Fav or Composition O ver Inheritanc e 

Favor Composition Over Inheritance

Inheritance is probably the most obvious and easy way of reusing code between classes. You have two classes with the same code. Create a common base class for these two and move the similar code into it. Piece of cake!

Unfortunately, inheritance comes with caveats that often become apparent only after your program already has tons of classes and changing anything is pretty hard. Here’s a list of those problems.

- **A subclass can’t reduce the interface of the superclass**. You have to implement all abstract methods of the parent class even if you won’t be using them.
- **When overriding methods you need to make sure that the new behavior is compatible with the base one**. It’s important because objects of the subclass may be passed to any code that expects objects of the superclass and you don’t want that code to break.
- **Inheritance breaks encapsulation of the superclass** because the internal details of the parent class become available to the subclass. There might be an opposite situation where a pro- grammer makes a superclass aware of some details of sub- classes for the sake of making further extension easier.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
48  ![](Output.019.png)Design Principles / Fav or Composition O ver Inheritanc e 
- **Subclasses are tightly coupled to superclasses**. Any change in a superclass may break the functionality of subclasses.
- **Trying to reuse code through inheritance can lead to creat- ing parallel inheritance hierarchies**. Inheritance usually takes place in a single dimension. But whenever there are two or more dimensions, you have to create lots of class combina- tions, bloating the class hierarchy to a ridiculous size.

There’s an alternative to inheritance called *composition*. Whereas inheritance represents the “is a” relationship between classes (a car *is a* transport), composition represents the “has a” relationship (a car *has an* engine).

I should mention that this principle also applies to aggrega- tion—a more relaxed variant of composition where one object may have a reference to the other one but doesn’t manage its lifecycle. Here’s an example: a car *has a* driver, but he or she may use another car or just walk *without the car*.

Example

Imagine that you need to create a catalog app for a car manu- facturer. The company makes both cars and trucks; they can be either electric or gas; all models have either manual controls or an autopilot.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
49  ![](Output.012.png)Design Principles / Fav or Composition O ver Inheritanc e 

![](Output.032.png)

*INHERITANCE: extending a class in several dimensions (cargo type × engine type × navigation type) may lead to a combinatorial explosion of subclasses.*

As you see, each additional parameter results in multiply- ing the number of subclasses. There’s a lot of duplicate code between subclasses because a subclass can’t extend two class- es at the same time.

You can solve this problem with composition. Instead of car objects implementing a behavior on their own, they can dele- gate it to other objects.

The added benefit is that you can replace a behavior at run- time. For instance, you can replace an engine object linked to a car object just by assigning a different engine object to the car.

**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
50  ![](Output.005.png)Design Principles / Fav or Composition O ver Inheritanc e 

![](Output.033.png)

*COMPOSITION: different “dimensions” of functionality extracted to their own class hierarchies.*

This structure of classes resembles the *Strategy* pattern, which we’ll go over later in this book.

**This document was truncated here because it was created in the Evaluation Mode.**

**This document was truncated here because it was created in the Evaluation Mode.**

**This document was truncated here because it was created in the Evaluation Mode.**
**Created with an evaluation copy of Aspose.Words. To discover the full versions of our APIs please visit: https://products.aspose.com/words/**

*programmer290399@gmail.com (#98645)*
