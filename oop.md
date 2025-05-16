# What Is Object-Oriented Programming in Python?
Object-oriented programming is a programming paradigm that provides a means of structuring programs so that properties and behaviors are bundled into individual objects.

For example, an object could represent a person with properties like a name, age, and address and behaviors such as walking, talking, breathing, and running. Or it could represent an email with properties like a recipient list, subject, and body and behaviors like adding attachments and sending.

Put another way, object-oriented programming is an approach for modeling concrete, real-world things, like cars, as well as relations between things, like companies and employees or students and teachers. OOP models real-world entities as software objects that have some data associated with them and can perform certain operations.

OOP also exists in other programming languages and is often described to center around the four pillars, or four tenants of OOP:

1. Encapsulation allows you to bundle data (attributes) and behaviors (methods) within a class to create a cohesive unit. By defining methods to control access to attributes and its modification, encapsulation helps maintain data integrity and promotes modular, secure code.
2. Inheritance enables the creation of hierarchical relationships between classes, allowing a subclass to inherit attributes and methods from a parent class. This promotes code reuse and reduces duplication.
3. Abstraction focuses on hiding implementation details and exposing only the essential functionality of an object. By enforcing a consistent interface, abstraction simplifies interactions with objects, allowing developers to focus on what an object does rather than how it achieves its functionality.
4. Polymorphism allows you to treat objects of different types as instances of the same base type, as long as they implement a common interface or behavior. Python’s duck typing make it especially suited for polymorphism, as it allows you to access attributes and methods on objects without needing to worry about their actual class.
## How Do You Define a Class in Python?
In Python, you define a class by using the class keyword followed by a name and a colon. Then you use .```__init__()``` to declare which attributes each instance of the class should have:
```python
class Employee:
    def __init__(self, name, age):
        self.name =  name
        self.age = age
```
But what does all of that mean? And why do you even need classes in the first place? Take a step back and consider using built-in, primitive data structures as an alternative.

Primitive data structures—like numbers, strings, and lists—are designed to represent straightforward pieces of information, such as the cost of an apple, the name of a poem, or your favorite colors, respectively. What if you want to represent something more complex?

For example, you might want to track employees in an organization. You need to store some basic information about each employee, such as their name, age, position, and the year they started working.

One way to do this is to represent each employee as a list:
```python
kirk = ["James Kirk", 34, "Captain", 2265]
spock = ["Spock", 35, "Science Officer", 2254]
mccoy = ["Leonard McCoy", "Chief Medical Officer", 2266]
```
There are a number of issues with this approach.

First, it can make larger code files more difficult to manage. If you reference ```kirk[0]``` several lines away from where you declared the kirk list, will you remember that the element with index 0 is the employee’s name?

Second, it can introduce errors if employees don’t have the same number of elements in their respective lists. In the ```mccoy list``` above, the age is missing, so ```mccoy[1]``` will return "Chief Medical Officer" instead of Dr. McCoy’s age.

A great way to make this type of code more manageable and more maintainable is to use classes.

## Classes vs Instances
Classes allow you to create user-defined data structures. Classes define functions called methods, which identify the behaviors and actions that an object created from the class can perform with its data.

In this tutorial, you’ll create a Dog class that stores some information about the characteristics and behaviors that an individual dog can have.

A class is a blueprint for how to define something. It doesn’t actually contain any data. The Dog class specifies that a name and an age are necessary for defining a dog, but it doesn’t contain the name or age of any specific dog.

While the class is the blueprint, an instance is an object that’s built from a class and contains real data. An instance of the Dog class is not a blueprint anymore. It’s an actual dog with a name, like Miles, who’s four years old.

Put another way, a class is like a form or questionnaire. An instance is like a form that you’ve filled out with information. Just like many people can fill out the same form with their own unique information, you can create many instances from a single class.

## Class Definition
You start all class definitions with the class keyword, then add the name of the class and a colon. Python will consider any code that you indent below the class definition as part of the class’s body.

### Here’s an example of a Dog class:

`dog.py`

```python
class Dog:
    pass
````

The body of the Dog class consists of a single statement: the pass keyword. Python programmers often use pass as a placeholder indicating where code will eventually go. It allows you to run this code without Python throwing an error.

The Dog class isn’t very interesting right now, so you’ll spruce it up a bit by defining some properties that all Dog objects should have. There are several properties that you can choose from, including name, age, coat color, and breed. To keep the example small in scope, you’ll just use name and age.

You define the properties that all Dog objects must have in a method called .```__init__()```. Every time you create a new Dog object, .```__init__()``` sets the initial state of the object by assigning the values of the object’s properties. That is, .```__init__()``` initializes each new instance of the class.

You can give .```__init__()``` any number of parameters, but the first parameter will always be a variable called self. When you create a new class instance, then Python automatically passes the instance to the self parameter in .```__init__()``` so that Python can define the new attributes on the object.

Update the Dog class with an .```__init__()``` method that creates .name and .age attributes:
`
dog.py`
```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```
Make sure that you indent the ```.__init__()``` method’s signature by four spaces, and the body of the method by eight spaces. This indentation is vitally important. It tells Python that the ```.__init__()``` method belongs to the Dog class.

In the body of ```.__init__()```, there are two statements using the self variable:

```self.name = name``` creates an attribute called name and assigns the value of the name parameter to it.
```self.age = age``` creates an attribute called age and assigns the value of the age parameter to it.
Attributes created in ```.__init__()``` are called instance attributes. An instance attribute’s value is specific to a particular instance of the class. All Dog objects have a name and an age, but the values for the name and age attributes will vary depending on the Dog instance.

On the other hand, class attributes are attributes that have the same value for all class instances. You can define a class attribute by assigning a value to a variable name outside of ```.__init__()```.

For example, the following Dog class has a class attribute called species with the value "Canis familiaris":

``dog.py``
```python
class Dog:
    species = "Canis familiaris"

    def __init__(self, name, age):
        self.name = name
        self.age = age
```
You define class attributes directly beneath the first line of the class name and indent them by four spaces. You always need to assign them an initial value. When you create an instance of the class, then Python automatically creates and assigns class attributes to their initial values.

Use class attributes to define properties that should have the same value for every class instance. Use instance attributes for properties that vary from one instance to another.
Here’s a `README.md` file based on your notes about class instantiation, attributes, and instance methods in Python:

# Python OOP: Instantiating Classes and Working with Attributes

## Instantiating a Class

To instantiate (create) a new object from a class, use the class name followed by parentheses:

```python
class Dog:
    pass

dog1 = Dog()
print(dog1)
````

This creates a new instance of `Dog`. The output shows the memory address of the object.

Creating multiple instances:

```python
a = Dog()
b = Dog()

print(a == b)  # False, because they are different instances
```

---

## Class and Instance Attributes

You can define both **class attributes** and **instance attributes**:

```python
class Dog:
    species = "Canis familiaris"  # Class attribute

    def __init__(self, name, age):  # Constructor
        self.name = name            # Instance attribute
        self.age = age              # Instance attribute
```

### Creating Dog Instances

```python
miles = Dog("Miles", 4)
buddy = Dog("Buddy", 9)
```

### Accessing Attributes

```python
print(miles.name)     # 'Miles'
print(miles.age)      # 4
print(buddy.species)  # 'Canis familiaris'
```

### Modifying Attributes

Instance attributes and class attributes can be changed dynamically:

```python
buddy.age = 10
print(buddy.age)      # 10

miles.species = "Felis silvestris"
print(miles.species)  # 'Felis silvestris'
```

---

## Instance Methods (Intro)

Instance methods are functions defined within a class and operate on an instance of that class using `self`. These methods can access and modify instance attributes.

```python
class Dog:
    species = "Canis familiaris"

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def speak(self, sound):
        return f"{self.name} says {sound}"
```

```python
miles = Dog("Miles", 4)
print(miles.speak("Woof"))  # "Miles says Woof"
```

---

## Key Takeaways

* Instantiating a class creates a unique object in memory.
* Use the `__init__()` method to initialize attributes.
* Class attributes are shared; instance attributes are unique.
* Objects are mutable and can have their attributes changed.
* Instance methods use `self` to interact with instance data.

---
Here's a clean, ad-free `README.md` based on your notes about class inheritance in Python:

# Python Inheritance: Reusing and Extending Classes

Inheritance allows you to create a new class that reuses the functionality of an existing class. It’s a cornerstone of Object-Oriented Programming (OOP) and helps reduce code duplication.

---

## Basic Inheritance

Child classes inherit attributes and methods from parent classes.

```python
class Parent:
    hair_color = "brown"

class Child(Parent):
    pass

print(Child.hair_color)  # Outputs: brown
````

In this example, the `Child` class automatically inherits the `hair_color` attribute from the `Parent` class.

---

## Overriding Inherited Attributes

Child classes can override attributes or methods defined in the parent class.

```python
class Parent:
    hair_color = "brown"

class Child(Parent):
    hair_color = "purple"

print(Child.hair_color)  # Outputs: purple
```

Here, the `Child` class overrides the `hair_color` inherited from `Parent`.

---

## Extending Parent Class Functionality

Child classes can also **extend** the functionality of the parent class by adding new methods or attributes.

```python
class Parent:
    speaks = ["English"]

class Child(Parent):
    def __init__(self):
        super().__init__()  # Call Parent's constructor if defined
        self.speaks.append("German")

child = Child()
print(child.speaks)  # Outputs: ['English', 'German']
```

---

## Example: Modeling a Dog Park

We can model dogs with a base class and differentiate behavior by subclassing.

### Base Class

```python
class Dog:
    species = "Canis familiaris"

    def __init__(self, name, age, breed):
        self.name = name
        self.age = age
        self.breed = breed

    def __str__(self):
        return f"{self.name} is {self.age} years old"

    def speak(self, sound):
        return f"{self.name} says {sound}"
```

### Instantiating Dogs

```python
miles = Dog("Miles", 4, "Jack Russell Terrier")
buddy = Dog("Buddy", 9, "Dachshund")
jack = Dog("Jack", 3, "Bulldog")
jim = Dog("Jim", 5, "Bulldog")
```

Calling the `.speak()` method:

```python
print(buddy.speak("Yap"))   # Buddy says Yap
print(jim.speak("Woof"))    # Jim says Woof
```

You must manually specify the `sound` argument. Later, you could use inheritance to create breed-specific dog classes with predefined sounds to simplify this.

---

## Key Takeaways

* Child classes inherit all methods and attributes from parent classes.
* You can override or extend behavior in child classes.
* Use `super().__init__()` to call a parent’s constructor when initializing child classes.
* Inheritance helps keep your code DRY (Don't Repeat Yourself) and organized.

---