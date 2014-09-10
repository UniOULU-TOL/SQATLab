% Refactoring
% with examples
% 

# Definition

> A **disciplined** technique for **restructuring** internal code without changing its **behaviour**, in order to fix **code smells**

# Code smell  
> Code that is not technically incorrect and do not currently prevent the program from functioning. Instead, they indicate weaknesses in design that may be slowing down development or increasing the risk of bugs or failures in the future. (Wikipedia)

> - A code smell is **NOT** a bug! 


# Refactoring catalog
[http://refactoring.com/catalog](http://refactoring.com/catalog)

# Consolidate conditionals
 - Multiple conditionals can be extracted into method(s)
 - They have the same result  

-------------------------------

### Consolidate conditionals example
**Before**

	Double disabilityAmount() {
		if (seniority < 2) return 0;
		if (monthsDisabled > 12) return 0;
		if (isPartTime) return 0;
		// compute the disability amount

**After**	

	Double disabilityAmount() {
		if (isNotEligableForDisability()) return 0;
		// compute the disability amount

# Extract class
 - You have a **God** class
 - Split it according to the data/intentions

----------------------------

### Extract class example
**Before**

	public class Person {
		String name;
		String officeAreaCode;
		String officeNumber;
		String getTelephoneNumber(){}

**After**	

	public class Person {
		String name;
		String getTelephoneNumber(){}

	public class TelephoneNumber {
		String officeAreaCode;
		String officeNumber;
		String getTelephoneNumber(){}

# Extract interface
- Many classes use the same subset of methods
- Many classes have methods in common

----------------------

### Extract interface example
**Before**

	public class Employee {
		Double getRate()
		boolean hasSpecialSkills()
		String getName()
		String getDept()

**After** 

	public interface Billable {
		Double getRate()
		boolean hasSpecialSkills()


	public class Employee implements Billable {
		Double getRate()
		boolean hasSpecialSkills()
		String getName()
		String getDept()


# Introduce parameter object
- The same parameters are used together
- Replace them with an object

--------------------------

### Introduce parameter object example
**Before**

	public class Customer {
		Double amountInvoiced(Date start, Date end)
		Double amountReceived(Date start, Date end)
		Double amountOverdue(Date start, Date end)

**After** 

	public class DateRange {
		Date start;
		Date end;
		boolean validDateRange()


	public class Customer {
		Double amountInvoiced(DateRange range)
		Double amountReceived(DateRange range)
		Double amountOverdue(DateRange range)

# Preserve whole object
- The same parameters are passed to a method
- Pass the whole object to the method

---------------------------------

### Preserve whole object example

**Before**

	DaysRange range = new DaysRange(int high, int low)
	...
	int low = range.getLow();
	int high = range.getHigh();
	this.withinRange(low, high);

**After** 

	this.withinRange(range);

# Parametrize method
- Many methods do similar things but with different values 
- Use a parameter to for the value

------------------------------

### Parametrize method example

**Before**

	Double fivePercentRaise(){}
	Double tenPercenRaise(){};
	
**After** 

	Double raise(int percentage)

# Replace parameter with method
- The result of a method is passed to another method 
- The receiver can also invoke the method

-----------------------------------

### Replace parameter with method example

**Before**

	int basePrice = quantity * itemPrice;
	int discount = calculateDiscount();
	Double finalPrice = discountedPrice(basePrice, discount)

**After** 

	int basePrice = quantity * itemPrice;
	Double finalPrice = discountedPrice(basePrice)

# Others
- Method should communicate its responsibility 
	- A clumsy method name *smells* bad 
- Extract *magic number* into constant
- **In general**
	- DRY (Don’t repeat yourself)
	- KISS (Keep it simple, stupid)

# TDD Randori
1. The pair
	- P1 writes a test that fails
	- P2 writes the implementation to pass
	
2. The audience
	- suggests refactoring 
  
> if GREEN && !timer.isOver then COMMIT  
 if RED && time.isOver then REVERT

