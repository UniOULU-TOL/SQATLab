% Intro to Mutation Testing
% Session 5

# Coverage tells you which part of the system is exercised by tests
# Unit-tests tell you about the quality of your code
# but...

-----------------------

Watchmen

------------------------

# Mutation testing
Evaluate the quality of tests by: 

> * modifying the program
> * using mutation operators
> * if the test fails it kills the mutant
> * if the test still pass the mutant survives

---------------------------

Before
 
    int max (int a, int b){
        return (a < b) ? b : a;
    }

After (_change conditional operators_)

    int max (int a, int b){
        return (a <= b) ? b : a;
    }

# Mutation problems
* Huge number of mutants
	* 500 classes
	* 20 tests per class
	* 10 mutants per class
	* 1 ms per test   
**13h 53m 20s**

* Equivalent mutant
	* Manual inspection

* Never ending mutants
	* Infinite loops 

* Hard to integrate into TDD

# Demo
PIT [http://pitest.org](http://pitest.org)