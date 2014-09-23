%SOLID Principles
%Session 3

# Remember code smells?
A code base tends to _rot_

> - Rigidity
> - Fragility
> - Immobility
> - Repetition
> - Opacity 

# Remember refactoring?
_Reconstruct_ the code in order to fix a code smell

> - What if I want to avoid code smell (or bad design)?
> - What if I want to make code more testable?
> - What if I want to make developers happy?

# S.O.L.I.D. code

An acronym made of acronyms 

> - **S**RP: Single Responsibility Principle
> - **O**CP: Open Closed Principle
> - **L**SP: Liskov Substitution Principle
> - **I**SP: Interface Segregation Principle
> - **D**IP: Dependency Inversion Principle

# SINGLE RESPONSIBILITY
> Just because you can, it does’t mean you should

----------------------------

### A class should:  

- **Serve a single purpose**
- **Have one, and one only, reason to change**

-------------------------------

### Use:
- Extract class/method
- Rename

--------------------------------------

**Bad example**  

	interface IEmail {
		public void setSender(String sender);
		public void setReceiver(String receiver);
		public void setContent(String content);
	}
	class Email implements IEmail {
		public void setSender(String sender) {// set sender; }
		public void setReceiver(String receiver) {// set receiver; }
		public void setContent(String content) {// set content; }
	}

--------------------------------------

**Good example**

	interface IEmail {
		public void setSender(String sender);
		public void setReceiver(String receiver);
		public void setContent(IContent content);
	}

	interface Content {
		public String getAsString(); // used for serialization
	}

	class Email implements IEmail {
		public void setSender(String sender) {// set sender; }
		public void setReceiver(String receiver) {// set receiver; }
		public void setContent(IContent content) {// set content; }
	}

# OPEN-CLOSED
> You don’t need brain surgery to put a hat on

-----------------------------

### A class should be:
- **Open for extension**
- **Closed for modification**

--------------------------------

### Use:
- Inheritance (_is-a_ relationship)
- Composition (_has-a_ relationship)

--------------------------------------

**Bad example**  

	class GraphicEditor {
 		public void drawShape(Shape s) {
			if (s.m_type==1) drawRectangle(s);
 			else if (s.m_type==2) drawCircle(s);
		}
		public void drawCircle(Circle r) {....}
		public void drawRectangle(Rectangle r) {....}
	}

	class Shape {
		int m_type;
	}

	class Rectangle extends Shape {
		Rectangle() {
 			super.m_type=1;
		}
	}

	class Circle extends Shape {
		Circle() {
			super.m_type=2;
		}
	}

--------------------------------------
 
**Good example**

	class GraphicEditor {
		public void drawShape(Shape s) {
			s.draw();
		}
	}
 
	interface Shape {
		void draw();
	}
 
	class Rectangle implements Shape  {
		public void draw() { // draw the rectangle}
	}

	class Circle implements Shape  {
		public void draw() { // draw the circle}
	} 

# LISKOV SUBSTITUTION
> If it looks like a duck and quacks like a duck but needs battery, you probably have the wrong abstraction

---------------------------------

### A (sub) class should:  
- **be substitutable for its base class**
- **not screw up the client code**

---------------------------------

### Use:
- Inheritance based on behaviour
- Do not violate behaviour of parent class

--------------------------------------

**Bad example**  
	
	class Rectangle {
		private int m_width;
		private int m_height;
		public void setWidth(int width){m_width = width;}
		public void setHeight(int height){m_height = height;}
		public int getWidth(){return m_width;}
		public int getHeight(){return m_height;}
		public int getArea(){return m_width * m_height;}	
	}
	
	class Square extends Rectangle {
		public void setWidth(int width){
			m_width = width;
			m_height = width;
		}
	}
		public void setHeight(int height){
			m_width = height;
			m_height = height;
		}
	}

	class LSPTest {
		private static Rectangle getNewRectangle(){
			return new Square();
	}

	public static void main (String args[]){
		Rectangle r = LSPTest.getNewRectangle();
		r.setWidth(5);
		r.setHeight(10);
		System.out.println(r.getArea());
		//The area is 100 instead of 50.
		}
	}

--------------------------------------
 
**Good example**

	class Rectangle {
		public void setHeight(int height)
		public void setWidth(int width)
		...
	}

	class Square {
		public void setWidth(int width)
	}


# Interface segregation
> Clients should not depend on interfaces they don’t use

------------------------------------


### An interface should be:  
- **fine grained**
- **client specific** 

-----------------------------------

### Use:
- Lean inheritance
- Don’t worry about adding a new Interface

--------------------------------------

**Bad example**  

	interface IWorker {
		public void work();
		public void eat();
	}

	class Worker implements IWorker{
		public void work() {// ....working}
		public void eat() {// ...... eating in launch break}
	}

	class SuperWorker implements IWorker {
		public void work() { //.... working much more}
		public void eat() { //.... eating in launch break}
	}

	class Manager {
		IWorker worker;
		public void setWorker(IWorker w) {worker=w;}
		public void manage() {
			worker.work();
		}
	}

--------------------------------------
 
**Good example**

	interface IWorkable {
		public void work();
	}

	interface IFeedable{
		public void eat();
	}

	class Worker implements IWorkable, IFeedable{
		public void work() {// ....working}
		public void eat() {//.... eating in launch break}
	}

	class Robot implements IWorkable{
		public void work() {// ....working}
	}

	class SuperWorker implements IWorkable, IFeedable{
		public void work() {//.... working much more}
		public void eat() {//.... eating in launch break}
	}


# Dependency Inversion
> Would you solder a lamp directly to the wall’s wires?

----------------------------------------

### A class should:
- **depend on abstractions**
- **do not depend on concretions**

-----------------------------------

### Use:  
- Dependency injection
- Aspect Oriented Programming

--------------------------------------

**Bad example**  

	class Worker {
		public void work() {// ....working}
	}

	class Manager {
		Worker worker;
		public void setWorker(Worker w) {worker = w;}
		public void manage() {worker.work();}
	}
	class SuperWorker {
		public void work() {//.... working much more}
	}

--------------------------------------
 
**Good example**

	interface IWorker {
		public void work();
	}

	class Worker implements IWorker{
		public void work() {// ....working}
	}

	class SuperWorker  implements IWorker{
		public void work() {//.... working much more}
	}

	class Manager {
		IWorker worker;
		public void setWorker(IWorker w) {worker = w;}
		public void manage() {worker.work();}
	}


# SOLID principles are **not** the silver bullet
# Apply when it makes **sense**
> - **Use your brain**

# SOLID principles help you to acquire OOD **habits** 

-----------------------------------

> I am not a great software engineer, I am a software engineer with great habits  
	(Kent Beck)