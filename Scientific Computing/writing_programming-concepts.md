# Programming concepts for Data Scientists

In this post I'll present some programming concepts for data science, specially for people without a background in programming or computer science. If you are becoming a data scientist but you don't such background, this post will help a lot. 

In this post, each concept will be defined theoretically but most of the times also will contain some practical and helpful things 
```
in boxes like these
```



Lets begin!
![[DALLE_2022-08-10_10.20.46_-_dall-e_trying_to_figure_out_how_dall-e_works.png]]

# Programming Basics

### Expression
An expression is a syntactic entity in a programming language that *may be evaluated* to determine its value. It's a combination of one or more constants, variables, functions, and operators that the programming language interprets (according to its particular rules of precedence and of association) and computes to produce ("to return", in a stateful environment) another value. 
In simple settings, the resulting value is usually one of various primitive types, such as numerical, string, boolean, complex data type or other types. 

Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (with a few exceptions in some programming languages like R or Julia).



### Syntax
The syntax of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. Applies to programming languages, source code and markup languages. 



### Primitive data types
Primitive data types are a set of basic data types from which all other data types are constructed. Specifically it often refers to the limited set of data representations in use by a particular processor, which all compiled programs must use. 



# Functions

A _function_ is a named sequence of statements that performs some useful operation. When you define a function, you specify the name and the sequence of statements. Later, you can “call” the function by name. Functions may or may not take arguments and may or may not produce a result. It is common to say that a function “takes” an argument and “returns” a result. The result is also called the _return value_.

Function definitions get executed just like other statements, but the effect is to create function objects. The statements inside the function do not run until the function is called, and the function definition generates no output.

As you might expect, you have to create a function before you can run it. In other words, the function definition has to run before the function gets called.

Inside the function, the arguments are assigned to variables called _parameters_. Here is a definition for a function that takes an argument:


### Infix operator
A function of two arguments, with the name of the function written between the arguments. e.g. `+` (yes, that's a function)




# Object oriented programming
Object-oriented programming (OOP) is a computer programming model that organizes software design around data, or objects, rather than functions and logic. An object can be defined as a data field that has unique attributes and behavior.
OOP focuses on the objects that developers want to manipulate rather than the logic required to manipulate them. This approach to programming is well-suited for programs that are large, complex and actively updated or maintained. This includes programs for manufacturing and design, as well as mobile applications




OOP (Object-oriented programming) is a programming paradigm based on the concept of "objects", which can contain data and code: data in the form of fields (often known as attributes or properties), and code, in the form of procedures (often known as methods).
A common feature of objects is that procedures (or methods) are attached to them and can access and modify the object's data fields. In this brand of OOP, there is usually a special name such as this or self used to refer to the current object. In OOP, computer programs are designed by making them out of objects that interact with one another.[1][2] OOP languages are diverse, but the most popular ones are class-based, meaning that objects are instances of classes, which also determine their types. 



### Constructor 
When a struct is used as a function for creating objects, it is called a constructor. Constructors return objects. 


### Instantiation 
Creating a new object is called _instantiation_, and the object is an _instance_ of the type.

When you print an instance, Julia tells you what type it belongs to and what the values of the atributes are.

Every object is an instance of some type, so “object” and “instance” are interchangeable. But in this chapter I use “instance” to indicate that I am talking about a programmer-defined type.


### Iterator
An iterable is an object that can be treated as a sequence.


# Other
### Scheduler
A program that arranges jobs or a computer's operations into an appropriate sequence. 
Schedulling is the action of assigning resources to perform tasks. The resources may be processors, or other things. The tasks may be threads, processes or data flows. The scheduler is the process that carries out the activity of scheduling.  
