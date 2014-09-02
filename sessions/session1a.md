% Unit-testing with JUnit
% 
% 

# JUnit
> JUnit is a **unit-testing** framework for the Java programming language (_Wikipedia_)

# Unit-testing
> The goal of unit testing is to **isolate** each part of the program and show that the individual parts are **correct**. A unit-test provides a strict, written **contract** that the piece of code must satisfy (_Wikipedia_)

-------------------------

![or is it?](dhh.png)

----------------------------

# What’s a unit?

> - A method?
> - An object?
> - Interaction between objects?

# Why testing?
![](why_testing.png)

# When stop testing?
> - you can provide better value by doing something else
> - you tested (everything) that could possibly break!
> - <strike>you reach 100% coverage</strike> 

# Code coverage
> a measure used to describe the degree to which the source code of a program is tested by a particular test suite (Wikipedia)

> - Function
> - Statement
> - Branch 
> - Condition

# A good test is...
> - Accurate
> - Independent
> - Reusable
> - Easy to run
> - Fast to run

# Unit-tests 3As 
> - **A**rrange
> - **A**ct
> - **A**ssert

# Assert
verb *\\ə-‘sərt, a-\\*

- to state smth in a strong and definite way
- to demand that other people accept or respect smth

# In JUnit...
> - Annotate a method with **@Test**
> - it has **public** access
> - it returns **void**
> - contains a call to an **assert** method

---------------------------

### optionally
> - fixture annotated with **@Before** and **@After**
> - can be grouped in a **Suite**
> - you can test your exceptions, too! **@Test(expected=Exception)**

# JUnit Asserts
- assertEquals()
- assertTrue()
- assertNull()
  

[Javadoc](http://junit.sourceforge.net/javadoc/org/junit/Assert.html)

# Shopping Cart
- add items
- remove items
- ask for total numbers of items
- ask for total price of items
- handle exception(s)

# Randori 
### (乱取り) 
in Japanese martial arts describes free-style practice

# SQAT Randori
- I will present an exercise
- A pair, from the audience, implements the exercise
- The pair **thinks aloud**
- Half of the pair swaps back to the audience every 5 mins
- The audience gives advices, asks for clarifications

