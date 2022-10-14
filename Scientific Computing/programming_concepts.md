
### Object introspection
Using a question mark (`?`) before or after a variable will display some general information about the object:

```
In [1]: b = [1, 2, 3]

In [2]: b?
Type:        list
String form: [1, 2, 3]
Length:      3
Docstring:
Built-in mutable sequence.

If no argument is given, the constructor creates a new empty list.
The argument must be an iterable if specified.
```
This is referred to as _object introspection_. If the object is a function or instance method, the docstring, if defined, will also be shown. Suppose we’d written the following function (which you can reproduce in IPython or Jupyter)

`?` has a final usage, which is for searching the IPython namespace in a manner similar to the standard Unix or Windows command line. A number of characters combined with the wildcard (`*`) will show all names matching the wildcard expression. For example, we could get a list of all functions in the top-level NumPy namespace containing `load`:

```
In [9]: import numpy as np

In [10]: np.*load*?
np.__loader__
np.load
np.loads
np.loadtxt
```

### Typed language
Typed Language: Typed languages are **the languages in which we define the type of data type and it will be known by machine at the compile-time or at runtime**. Typed languages can be classified into two categories: Statically typed languages. Dynamically typed languages


### Dynamically typed language
Dynamically-typed languages are those (like Julia) where the interpreter assigns variables a type at runtime based on the variable's value at the time.


### Statically typed



### Duck typing
wiki
**Duck typing** in computer programming is an application of the [duck test](https://en.wikipedia.org/wiki/Duck_test "Duck test")—"If it walks like a duck and it quacks like a duck, then it must be a duck"—to determine whether an [object](https://en.wikipedia.org/wiki/Object_(computer_science) "Object (computer science)") can be used for a particular purpose. With [nominative typing](https://en.wikipedia.org/wiki/Nominative_typing "Nominative typing"), an object is _of a given type_ if it is declared to be (or if a type's association with the object is inferred through mechanisms such as [object inheritance](https://en.wikipedia.org/wiki/Object_inheritance "Object inheritance")). In duck typing, an object is _of a given type_ if it has all [methods](https://en.wikipedia.org/wiki/Method_(computer_programming) "Method (computer programming)") and properties required by that type.[[1]](https://en.wikipedia.org/wiki/Duck_typing#cite_note-1)[[2]](https://en.wikipedia.org/wiki/Duck_typing#cite_note-2) Duck typing can be viewed as a usage-based structural equivalence between a given object and the requirements of a type. See [structural typing](https://en.wikipedia.org/wiki/Structural_typing "Structural typing") for a further explanation of structural type equivalence.

This is a simple example in [Python](https://en.wikipedia.org/wiki/Python_(programming_language) "Python (programming language)") 3 that demonstrates how any object may be used in any context, up until it is used in a way that it does not support.

class Duck:
    def swim(self):
        print("Duck swimming")

    def fly(self):
        print("Duck flying")

class Whale:
    def swim(self):
        print("Whale swimming")

for animal in [Duck(), Whale()]:
    animal.swim()
    animal.fly()

Output:

Duck swimming
Duck flying
Whale swimming
AttributeError: 'Whale' object has no attribute 'fly'

So, if we assume everything that can swim is a duck because ducks can swim, we will consider a whale to be a duck, but, if we also assume it has to be capable of flying, the whale won’t be considered to be a duck.


end wiki

wes mckinley book
Often you may not care about the type of an object but rather only whether it has certain methods or behavior. This is sometimes called _duck typing_, after the saying "If it walks like a duck and quacks like a duck, then it's a duck." For example, you can verify that an object is iterable if it implements the _iterator protocol_. For many objects, this means it has an `__iter__` “magic method,” though an alternative and better way to check is to try using the `iter` function:

```
In [33]: def isiterable(obj):
   ....:     try:
   ....:         iter(obj)
   ....:         return True
   ....:     except TypeError: # not iterable
   ....:         return False
```

This function would return `True` for strings as well as most Python collection types:

```
In [34]: isiterable("a string")
Out[34]: True

In [35]: isiterable([1, 2, 3])
Out[35]: True

In [36]: isiterable(5)
Out[36]: False
```
end book

### Casting
changing the type of an object, automatically?

### Callback: 
	FROM WIKIPEDIA
In computer programming, a callback, also known as a "call-after" function, is **any reference to executable code that is passed as an argument to other code; that other code is expected to call back (execute) the code at a given time**.

	FROM https://stackoverflow.com/questions/9596276/how-to-explain-callbacks-in-plain-english-how-are-they-different-from-calling-o?page=1&tab=trending#tab-top

In plain English, a callback function is like a **Worker** who "calls back" to his **Manager** when he has completed a **Task**.



--
am going to try to keep this dead simple. A "callback" is any function that is called by another function which takes the first function as a parameter. A lot of the time, a "callback" is a function that is called when _something_ happens. That _something_ can be called an "event" in programmer-speak.

Imagine this scenario: you are expecting a package in a couple of days. The package is a gift for your neighbor. Therefore, once you get the package, you want it brought over to the neighbors. You are out of town, and so you leave instructions for your spouse.

You could tell them to get the package and bring it to the neighbors. If your spouse was as stupid as a computer, they would sit at the door and wait for the package until it came (NOT DOING ANYTHING ELSE) and then once it came they would bring it over to the neighbors. But there's a better way. Tell your spouse that ONCE they receive the package, they should bring it over the neighbors. Then, they can go about life normally UNTIL they receive the package.

In our example, the receiving of the package is the "event" and the bringing it to the neighbors is the "callback". Your spouse "runs" your instructions to bring the package over only _when_ the package arrives. Much better!

This kind of thinking is obvious in daily life, but computers don't have the same kind of common sense. Consider how programmers normally write to a file:

```
fileObject = open(file)
# now that we have WAITED for the file to open, we can write to it
fileObject.write("We are writing to the file.")
# now we can continue doing the other, totally unrelated things our program does
```

Here, we WAIT for the file to open, before we write to it. This "blocks" the flow of execution, and our program cannot do any of the other things it might need to do! What if we could do this instead:

```
# we pass writeToFile (A CALLBACK FUNCTION!) to the open function
fileObject = open(file, writeToFile)
# execution continues flowing -- we don't wait for the file to be opened
# ONCE the file is opened we write to it, but while we wait WE CAN DO OTHER THINGS!
```

It turns out we do this with some languages and frameworks. It's pretty cool! Check out [Node.js](http://nodejs.org/) to get some real practice with this kind of thinking.



# Programming Basics

### Expression
An expression is a syntactic entity in a programming language that *may be evaluated* to determine its value. It's a combination of one or more constants, variables, functions, and operators that the programming language interprets (according to its particular rules of precedence and of association) and computes to produce ("to return", in a stateful environment) another value. 
In simple settings, the resulting value is usually one of various primitive types, such as numerical, string, boolean, complex data type or other types. 

Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (with a few exceptions in some programming languages like R or Julia).



### Syntax
The syntax of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. Applies to programming languages, source code and markup languages. 



### Primitive data types
Primitive data types are a set of basic data types from which all other data types are constructed. Specifically it often refers to the limited set of data representations in use by a particular processor, which all compiled programs must use. 



### Infix operator
A function of two arguments, with the name of the function written between the arguments. e.g. `+` (yes, that's a function)



### Scheduler
A program that arranges jobs or a computer's operations into an appropriate sequence. 
Schedulling is the action of assigning resources to perform tasks. The resources may be processors, or other things. The tasks may be threads, processes or data flows. The scheduler is the process that carries out the activity of scheduling.  



### Constructor 
When a struct is used as a function for creating objects, it is called a constructor. Constructors return objects. 




### Instantiation 
Creating a new object is called _instantiation_, and the object is an _instance_ of the type.

When you print an instance, Julia tells you what type it belongs to and what the values of the atributes are.

Every object is an instance of some type, so “object” and “instance” are interchangeable. But in this chapter I use “instance” to indicate that I am talking about a programmer-defined type.




### Object Diagram
A state diagram that shows an object and its fields is called an _object diagram_
![[Pasted image 20220716160338.png]]





### Iterator
An iterable is an object that can be treated as a sequence.




### Function
A named sequence of statements that performs some useful operation. Functions may or may not take arguments and may or may not produce a result.

In the context of programming, a _function_ is a named sequence of statements that performs a computation. When you define a function, you specify the name and the sequence of statements. Later, you can “call” the function by name.

The expression in parentheses is called the _argument_ of the function

It is common to say that a function “takes” an argument and “returns” a result. The result is also called the _return value_.

A _function definition_ specifies the name of a new function and the sequence of statements that run when the function is called.

The empty parentheses after the name indicate that this function doesn’t take any arguments.

The first line of the function definition is called the _header_; the rest is called the _body_. The body is terminated with the keyword `end` and it can contain any number of statements. For readability the body of the function should be indented.

Function definitions get executed just like other statements, but the effect is to create function objects. The statements inside the function do not run until the function is called, and the function definition generates no output.

As you might expect, you have to create a function before you can run it. In other words, the function definition has to run before the function gets called.

Inside the function, the arguments are assigned to variables called _parameters_. Here is a definition for a function that takes an argument:

```julia 
function printtwice(bruce)
    println(bruce)
    println(bruce)
end
```

This function assigns the argument to a parameter named `bruce`. When the function is called, it prints the value of the parameter (whatever it is) twice.

```
julia> printtwice("Spam "^4)
Spam Spam Spam Spam
Spam Spam Spam Spam
julia> printtwice(cos(π))
-1.0
-1.0
```
The argument is evaluated before the function is called, so in the examples the expressions `"Spam "^4` and `cos(π)` are only evaluated once.

You can also use a variable as an argument:

```
julia> michael = "Eric, the half a bee."
"Eric, the half a bee."
julia> printtwice(michael)
Eric, the half a bee.
Eric, the half a bee.
```

The name of the variable we pass as an argument (`michael`) has nothing to do with the name of the parameter (`bruce`). It doesn’t matter what the value was called back home (in the caller); here in `printtwice`, we call everybody `bruce`.



**Variables and parameters are local**
When you create a variable inside a function, it is _local_, which means that it only exists inside the function. For example:

```
function cattwice(part1, part2)
    concat = part1 * part2
    printtwice(concat)
end
```

This function takes two arguments, concatenates them, and prints the result twice. Here is an example that uses it:

```
julia> line1 = "Bing tiddle "
"Bing tiddle "
julia> line2 = "tiddle bang."
"tiddle bang."
julia> cattwice(line1, line2)
Bing tiddle tiddle bang.
Bing tiddle tiddle bang.
```

When `cattwice` terminates, the variable `concat` is destroyed. If we try to print it, we get an exception:

```
julia> println(concat)
ERROR: UndefVarError: concat not defined
```

Parameters are also local. For example, outside `printtwice`, there is no such thing as `bruce`.



#### Function definition
A statement that creates a new function, specifying its name, parameters, and the statements it contains.




#### Function object
A value created by a function definition. The name of the function is a variable that refers to a function object.


#### Local variable
A variable defined inside a function. A local variable can only be used inside its function.


#### Return value
The result of a function. If a function call is used as an expression, the return value is the value of the expression.



### Function Signature
A function signature (or type signature, or method signature) **defines input and output of functions or methods**. A signature can include: parameters and their types. a return value and type. exceptions that might be thrown or passed back



### Generic Functions
functions that can have more than one method


### Function method
the method of a function is the code in its code body


### Flow of execution
The order statements run in.

the order in which the statements are run is called the _flow of execution_.

Execution always begins at the first statement of the program. Statements are run one at a time, in order from top to bottom.

Function definitions do not alter the flow of execution of the program, but remember that statements inside the function don’t run until the function is called.

A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, runs the statements there, and then comes back to pick up where it left off.

In summary, when you read a program, you don’t always want to read from top to bottom. Sometimes it makes more sense if you follow the flow of execution.




### Stack Diagram
A graphical representation of a stack of functions, their variables, and the values they refer to.

To keep track of which variables can be used where, it is sometimes useful to draw a _stack diagram_. Like state diagrams, stack diagrams show the value of each variable, but they also show the function each variable belongs to.

Each function is represented by a _frame_. A frame is a box with the name of a function beside it and the parameters and variables of the function inside it. The stack diagram for the previous example is shown below

![[Pasted image 20220729121101.png]]

The frames are arranged in a stack that indicates which function called which, and so on. In this example, `printtwice` was called by `cattwice`, and `cattwice` was called by `Main`, which is a special name for the topmost frame. When you create a variable outside of any function, it belongs to `Main`.

Each parameter refers to the same value as its corresponding argument. So, `part1` has the same value as `line1`, `part2` has the same value as `line2`, and `bruce` has the same value as `concat`.

If an error occurs during a function call, Julia prints the name of the function, the name of the function that called it, and the name of the function that called _that_, all the way back to `Main`.

For example, if you try to access `concat` from within `printtwice`, you get a `UndefVarError`:
```
ERROR: UndefVarError: concat not defined
Stacktrace:
 [1] printtwice at ./REPL[1]:2 [inlined]
 [2] cattwice(::String, ::String) at ./REPL[2]:3
```

This list of functions is called a _stacktrace_. It tells you what program file the error occurred in, and what line, and what functions were executing at the time. It also shows the line of code that caused the error.

The order of the functions in the stacktrace is the inverse of the order of the frames in the stack diagram. The function that is currently running is at the top.

#### Stacktrace
A list of the functions that are executing, printed when an exception occurs.



#### Fruitful functions
A function that returns a value.

Some of the functions we have used, such as the math functions, return results; for lack of a better name, I call them _fruitful functions_.

When you call a fruitful function, you almost always want to do something with the result; for example, you might assign it to a variable or use it as part of an expression


When you call a function in interactive mode, Julia displays the result. But in a script, if you call a fruitful function all by itself, the return value is lost forever!



#### Void functions
A function that always returns `nothing`.

Other functions, like `printtwice`, perform an action but don’t return a value. They are called _void functions_.

Void functions might display something on the screen or have some other effect, but they don’t have a return value. If you assign the result to a variable, you get a special value called `nothing`.

(in julia) To print the value `nothing`, you have to use the function `show` which is like `print` but can handle the value `nothing`.



### Scope (in relation to functions)
The term scope refers to which variables can be accessed in a particular block of code (the program as a whole is also a code block). Scope can be global (to the whole program) or local (to a particular code block)

### Global variables
variables that are accessible to the whole program 

### Local variables
Some code blocks introduce a local scope. A local variable is one that cannot be accessed by code outside the code block that introduces the local scope.



### Why Functions
It may not be clear why it is worth the trouble to divide a program into functions. There are several reasons:

-   Creating a new function gives you an opportunity to name a group of statements, which makes your program easier to read and debug.
    
-   Functions can make a program smaller by eliminating repetitive code. Later, if you make a change, you only have to make it in one place.
    
-   Dividing a long program into functions allows you to debug the parts one at a time and then assemble them into a working whole.
    
-   Well-designed functions are often useful for many programs. Once you write and debug one, you can reuse it.
    
-   In Julia, functions can improve performance a lot.


### Composition
Using an expression as part of a larger expression, or a statement as part of a larger statement.


### Casting
Casting is a way to convert values from one type to another. Mainly, two types of casting exist, Implicit casting and Explicit casting. Boxing occurs when a value type is cast to an object, or reference type. 

equivalent to type conversion?



### Generator
something that will give a list of items when asked to (i.e., object = generator())



### Program
A _program_ is a sequence of instructions that specifies how to perform a computation. The computation might be something mathematical, such as solving a system of equations or finding the roots of a polynomial, but it can also be a symbolic computation, such as searching for and replacing text in a document, or something graphical, like processing an image or playing a video.


### Values
A _value_ is one of the basic things a program works with, like a letter or a number.
One of the basic units of data, like a number or string, that a program manipulates.


### Type 
A category of values.

### Operator
A symbol that represents a simple computation like addition, multiplication, or string concatenation.

### Operand 
One of the values on which an operator operates.


### Natural language
_Natural languages_ are the languages people speak, such as English, Spanish, and French. They were not designed by people (although people try to impose some order on them); they evolved naturally.



### Formal language
_Formal languages_ are languages that are designed by people for specific applications. For example, the notation that mathematicians use is a formal language that is particularly good at denoting relationships among numbers and symbols. Chemists use a formal language to represent the chemical structure of molecules. And most importantly, **programming languages are formal languages** that have been designed to express computations.


Formal languages tend to have strict _syntax_ rules that govern the structure of statements. For example, in mathematics the statement 3+3=6 has correct syntax, but 3+=3$6 does not. In chemistry, H2O is a syntactically correct formula, but 2Zz is not.

#### Formal language: Tokens
Syntax rules come in two flavors, pertaining to _tokens_ and _structure_. Tokens are the basic elements of the language, such as words, numbers, and chemical elements. One of the problems with 3+=3$6 is that $ is not a legal token in mathematics (at least as far as I know). Similarly, 2Zz is not legal because there is no element with the abbreviation Zz.

One of the basic elements of the syntactic structure of a program, analogous to a word in a natural language.

#### Formal language: Structure
The second type of syntax rule pertains to the way tokens are combined. The equation 3+=3 is illegal because even though + and = are legal tokens, you can’t have one right after the other. Similarly, in a chemical formula the subscript comes after the element name, not before.

This is @ well-structured Engli$h sentence with invalid t*kens in it. This sentence all valid tokens has, but invalid structure with.


#### Formal vs Natural languages
Although formal and natural languages have many features in common—tokens, structure, and syntax—there are some differences:


Ambiguity

Natural languages are full of ambiguity, which people deal with by using contextual clues and other information. Formal languages are designed to be nearly or completely unambiguous, which means that any statement has exactly one meaning, regardless of context.

Redundancy

In order to make up for ambiguity and reduce misunderstandings, natural languages employ lots of redundancy. As a result, they are often verbose. Formal languages are less redundant and more concise.

Literalness

Natural languages are full of idiom and metaphor. If I say, “The penny dropped,” there is probably no penny and nothing dropping (this idiom means that someone understood something after a period of confusion). Formal languages mean exactly what they say.

Because we all grow up speaking natural languages, it is sometimes hard to adjust to formal languages. 

Programs

The meaning of a computer program is unambiguous and literal, and can be understood entirely by analysis of the tokens and structure.

Formal languages are more dense than natural languages, so it takes longer to read them. Also, the structure is important, so it is not always best to read from top to bottom, left to right. Instead, you’ll learn to parse the program in your head, identifying the tokens and interpreting the structure. Finally, the details matter. Small errors in spelling and punctuation, which you can get away with in natural languages, can make a big difference in a formal language.


## Errors
Three kinds of errors can occur in a program: syntax errors, runtime errors, and semantic errors. It is useful to distinguish between them in order to track them down more quickly.

#### Syntax error
An error in a program that makes it impossible to parse (and therefore impossible to interpret).

“Syntax” refers to the structure of a program and the rules about that structure. For example, parentheses have to come in matching pairs, so `(1 + 2)` is legal, but `8)` is a syntax error.

If there is a syntax error anywhere in your program, Julia displays an error message and quits, and you will not be able to run the program. During the first few weeks of your programming career, you might spend a lot of time tracking down syntax errors. As you gain experience, you will make fewer errors and find them faster.


##### Left side of assignment operator
Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (we will see exceptions to this rule later).


#### Runtime error

The second type of error is a runtime error, so called because the error does not appear until after the program has started running. These errors are also called _exceptions_ because they usually indicate that something exceptional (and bad) has happened.

Runtime errors are rare in the simple programs you will see in the first few chapters, so it might be a while before you encounter one.

An error that is detected while the program is running.


#### Semantic error

The third type of error is “semantic”, which means related to meaning. If there is a semantic error in your program, it will run without generating error messages, but it will not do the right thing. It will do something else. Specifically, it will do what you told it to do.

Identifying semantic errors can be tricky because it requires you to work backward by looking at the output of the program and trying to figure out what it is doing.


An error in a program that makes it do something other than what the programmer intended

semantics is The meaning of a program.

----------------------------------------------------
Concepts from Think Julia https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#chap19

FALTA DE 3 A 14!

### Syntax

The rules that govern the structure of a program.


### Parsing
To examine a program and analyze the syntactic structure.


### Variable
A variable is a name that refers to a value.


### Assignment statement
An _assignment statement_ creates a new variable and gives it a value



### State diagram

A common way to represent variables on paper is to write the name with an arrow pointing to its value. This kind of figure is called a _state diagram_ because it shows what state each of the variables is in (think of it as the variable’s state of mind).
![[Pasted image 20220716150428.png]]




### Syntax error
If you give a variable an illegal name, you get a syntax error



### Expression
An _expression_ is a combination of values, variables, and operators. A value all by itself is considered an expression, and so is a variable

When you type an expression at the prompt, the REPL _evaluates_ it, which means that it finds the value of the expression. In this example, `n` has the value 17 and `n + 25` has the value 42.


### Evaluate
To simplify an expression by performing the operations in order to yield a single value.


#### Statements

When you type a statement, the REPL _executes_ it, which means that it does whatever the statement says
A section of code that represents a command or action. So far, the statements we have seen are assignments and print statements

### Execute 
To run a statement and do what it says.


### Interactive mode 
So far we have run Julia in _interactive mode_, which means that you interact directly with the REPL. Interactive mode is a good way to get started, but if you are working with more than a few lines of code, it can be clumsy.


### Script mode
The alternative is to save code in a file called a _script_ and then run Julia in _script mode_ to execute the script. By convention, Julia scripts have names that end with _.jl_.


... But if you type the same code into a script and run it, you get no output at all. In script mode an expression, all by itself, has no visible effect. Julia actually evaluates the expression, but it doesn’t display the value unless you tell it to with a print statement ...

### Operator precedence
When an expression contains more than one operator, the order of evaluation depends on the _operator precedence_.


### Comments

Everything from the `#` (in julia, other programming languages have other symbols) to the end of the line is ignored—it has no effect on the execution of the program.

Comments are most useful when they document non-obvious features of the code. It is reasonable to assume that the reader can figure out _what_ the code does; it is more useful to explain _why_.


### Concatenate
To join two strings end-to-end.


### Debugging

Three kinds of errors can occur in a program: syntax errors, runtime errors, and semantic errors. It is useful to distinguish between them in order to track them down more quickly.

#### Syntax error
An error in a program that makes it impossible to parse (and therefore impossible to interpret).

“Syntax” refers to the structure of a program and the rules about that structure. For example, parentheses have to come in matching pairs, so `(1 + 2)` is legal, but `8)` is a syntax error.

If there is a syntax error anywhere in your program, Julia displays an error message and quits, and you will not be able to run the program. During the first few weeks of your programming career, you might spend a lot of time tracking down syntax errors. As you gain experience, you will make fewer errors and find them faster.


##### Left side of assignment operator
Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (we will see exceptions to this rule later).


#### Runtime error

The second type of error is a runtime error, so called because the error does not appear until after the program has started running. These errors are also called _exceptions_ because they usually indicate that something exceptional (and bad) has happened.

Runtime errors are rare in the simple programs you will see in the first few chapters, so it might be a while before you encounter one.

An error that is detected while the program is running.


#### Semantic error

The third type of error is “semantic”, which means related to meaning. If there is a semantic error in your program, it will run without generating error messages, but it will not do the right thing. It will do something else. Specifically, it will do what you told it to do.

Identifying semantic errors can be tricky because it requires you to work backward by looking at the output of the program and trying to figure out what it is doing.


An error in a program that makes it do something other than what the programmer intended

semantics is The meaning of a program.



#### Debugging Practical
In some ways debugging is like detective work. You are confronted with clues and you have to infer the processes and events that led to the results you see.

Debugging is also like an experimental science. Once you have an idea about what is going wrong, you modify your program and try again. If your hypothesis was correct, you can predict the result of the modification, and you take a step closer to a working program. If your hypothesis was wrong, you have to come up with a new one. As Sherlock Holmes pointed out,

> When you have eliminated the impossible, whatever remains, however improbable, must be the truth.
— A. Conan Doyle




### Flow of execution 
To ensure that a function is defined before its first use, you have to know the order statements run in, which is called the _flow of execution_.

Execution always begins at the first statement of the program. Statements are run one at a time, in order from top to bottom.

Function definitions do not alter the flow of execution of the program, but remember that statements inside the function don’t run until the function is called.

A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, runs the statements there, and then comes back to pick up where it left off.




### Encapsulation
The process of transforming a sequence of statements into a function definition.

Wrapping a piece of code up in a function is called _encapsulation_. One of the benefits of encapsulation is that it attaches a name to the code, which serves as a kind of documentation. Another advantage is that if you re-use the code, it is more concise to call a function twice than to copy and paste the body!


### Generalization
The process of replacing something unnecessarily specific (like a number) with something appropriately general (like a variable or parameter).

Adding a parameter to a function is called _generalization_ because it makes the function more general: in the previous version, the square is always the same size; in this version it can be any size.


### Interface Design

A description of how to use a function, including the name and descriptions of the arguments and return value.

The _interface_ of a function is a summary of how it is used: what are the parameters? What does the function do? And what is the return value? An interface is “clean” if it allows the caller to do what they want without dealing with unnecessary details.


### Refactoring
The process of modifying a working program to improve function interfaces and other qualities of the code.

This process—rearranging a program to improve interfaces and facilitate code re-use—is called _refactoring_
... often you don’t know enough at the beginning of a project to design all the interfaces. Once you start coding, you understand the problem better. Sometimes refactoring is a sign that you have learned something.


### Development Plan

A _development plan_ is a process for writing programs.

#### Development Plan: Encapsulation and generalization

The steps of this process are:

1.  Start by writing a small program with no function definitions.
    
2.  Once you get the program working, identify a coherent piece of it, encapsulate the piece in a function and give it a name.
    
3.  Generalize the function by adding appropriate parameters.
    
4.  Repeat steps 1–3 until you have a set of working functions. Copy and paste working code to avoid retyping (and re-debugging).
    
5.  Look for opportunities to improve the program by refactoring. For example, if you have similar code in several places, consider factoring it into an appropriately general function.

This process has some drawbacks—we will see alternatives later—but it can be useful if you don’t know ahead of time how to divide the program into functions. This approach lets you design as you go along.


### Docstring
A string that appears at the top of a function definition to document the function’s interface.

A _docstring_ is a string before a function that explains the interface (“doc” is short for “documentation”). Here is an example:

```
"""
polyline(t, n, len, angle)

Draws n line segments with the given length and
angle (in degrees) between them.  t is a turtle.
"""
function polyline(t, n, len, angle)
    for i in 1:n
        forward(t, len)
        turn(t, -angle)
    end
end
```

Documentation can be accessed in the REPL or in a notebook by typing ? followed by the name of a function or macro, and pressing `ENTER`:

```
help?> polyline
search:

  polyline(t, n, len, angle)

  Draws n line segments with the given length and angle (in degrees) between them. t is a turtle.

```
A docstring contains the essential information someone would need to use this function. It explains concisely what the function does (without getting into the details of how it does it). It explains what effect each parameter has on the behavior of the function and what type each parameter should be (if it is not obvious).

Tip

Writing this kind of documentation is an important part of interface design. A well-designed interface should be simple to explain; if you have a hard time explaining one of your functions, maybe the interface could be improved.



#### Debugging (need to merge all debuggings)

An interface is like a contract between a function and a caller. The caller agrees to provide certain parameters and the function agrees to do certain work.

For example, `polyline` requires four arguments: `t` has to be a turtle; `n` has to be an integer; `len` should be a positive number; and `angle` has to be a number, which is understood to be in degrees.

These requirements are called _preconditions_ because they are supposed to be true before the function starts executing. Conversely, conditions at the end of the function are _postconditions_. Postconditions include the intended effect of the function (like drawing line segments) and any side effects (like moving the turtle or making other changes).

Preconditions are the responsibility of the caller. If the caller violates a (properly documented!) precondition and the function doesn’t work correctly, the bug is in the caller, not the function.

If the preconditions are satisfied and the postconditions are not, the bug is in the function. If your pre- and postconditions are clear, they can help with debugging.


#### Precondition
A requirement that should be satisfied by the caller before a function starts. 

#### Postcondition
A requirement that should be satisfied by the function before it ends. 

### Module
A file that contains a collection of related functions and other definitions.

### Package
An external library with additional functionality.

### Using statement
A statement that reads a module file and creates a module object.

### Loop
A part of a program that can run repeatedly.




### If statement

The `if` statement executes different code depending on the state of the program.


### Modulus operator
the _modulus operator_, `%`, which divides two numbers and returns the remainder.

```
julia> remainder = minutes % 60
45
```

Tip: The modulus operator is more useful than it seems. For example, you can check whether one number is divisible by another—if `x % y` is zero, then `x` is divisible by `y`.
Also, you can extract the right-most digit or digits from a number. For example, `x % 10` yields the right-most digit of an integer `x` (in base 10). Similarly `x % 100` yields the last two digits.

### Boolean Expressions
A _boolean expression_ is an expression that is either true or false. The following examples use the operator `==`, which compares two operands and produces `true` if they are equal and `false` otherwise:

```
julia> 5 == 5
true
julia> 5 == 6
false
```

`true` and `false` are special values that belong to the type `Bool`; they are not strings:

```
julia> typeof(true)
Bool
julia> typeof(false)
Bool
```



### Conditional Execution
In order to write useful programs, we almost always need the ability to check conditions and change the behavior of the program accordingly. _Conditional statements_ give us this ability. The simplest form is the `if` statement:

```julia
if x > 0
    println("x is positive")
end
```

The boolean expression after `if` is called the _condition_. If it is true, the indented statement runs. If not, nothing happens.

`if` statements have the same structure as function definitions: a header followed by body terminated with the keyword `end`. Statements like this are called _compound statements_.

There is no limit on the number of statements that can appear in the body. Occasionally, it is useful to have a body with no statements (usually as a place keeper for code you haven’t written yet).

```julia 
if x < 0
    # TODO: need to handle negative values!
end
```



### Alternative Execution
A second form of the `if` statement is “alternative execution”, in which there are two possibilities and the condition determines which one runs. The syntax looks like this:

```julia 
if x % 2 == 0
    println("x is even")
else
    println("x is odd")
end
```

If the condition is false, the second set of statements runs. Since the condition must be true or false, exactly one of the alternatives will run. The alternatives are called _branches_, because they are branches in the flow of execution.


### Chained conditionals
Sometimes there are more than two possibilities and we need more than two branches. One way to express a computation like that is a _chained conditional_:

```
if x < y
    println("x is less than y")
elseif x > y
    println("x is greater than y")
else
    println("x and y are equal")
end
```
Again, exactly one branch will run. There is no limit on the number of `elseif` statements. If there is an `else` clause, it has to be at the end, but there doesn’t have to be one.

```
if choice == "a"
    draw_a()
elseif choice == "b"
    draw_b()
elseif choice == "c"
    draw_c()
end
```

Each condition is checked in order. If the first is false, the next is checked, and so on. If one of them is true, the corresponding branch runs and the statement ends. Even if more than one condition is true, only the first true branch runs.

### Nested conditionals


One conditional can also be nested within another. We could have written the example in the previous section like this:

```
if x == y
    println("x and y are equal")
else
    if x < y
        println("x is less than y")
    else
        println("x is greater than y")
    end
end
```

The outer conditional contains two branches. The first branch contains a simple statement. The second branch contains another `if` statement, which has two branches of its own. Those two branches are both simple statements, although they could have been conditional statements as well.

Although the non-compulsory indentation of the statements makes the structure apparent, _nested conditionals_ become difficult to read very quickly. It is a good idea to avoid them when you can.


### Recursion
It is legal for one function to call another; it is also legal for a function to call itself. It may not be obvious why that is a good thing, but it turns out to be one of the most magical things a program can do. For example, look at the following function:

```
function countdown(n)
    if n ≤ 0
        println("Blastoff!")
    else
        print(n, " ")
        countdown(n-1)
    end
end
```

If `n` is 0 or negative, it outputs the word, `"Blastoff!"` Otherwise, it outputs `n` and then calls a function named `countdown`—itself—passing `n-1` as an argument.

What happens if we call this function like this?

```
julia> countdown(3)
3 2 1 Blastoff!
```

The execution of `countdown` begins with `n = 3`, and since `n` is greater than 0, it outputs the value 3, and then calls itself …​

 The execution of `countdown` begins with `n = 2`, and since `n` is greater than 0,  
  it outputs the value 2, and then calls itself …​

  The execution of `countdown` begins with `n = 1`, and since `n` is greater than 0,  
   it outputs the value 1, and then calls itself …​

   The execution of `countdown` begins with `n = 0`, and since `n` is not greater than  
    0, it outputs the word, `"Blastoff!"` and then returns.

  The countdown that got `n = 1` returns.

 The countdown that got `n = 2` returns.

The countdown that got `n = 3` returns.

And then you’re back in `Main`.

A function that calls itself is _recursive_; the process of executing it is called _recursion_.




### Infinite Recursion
If a recursion never reaches a base case, it goes on making recursive calls forever, and the program never terminates. This is known as _infinite recursion_, and it is generally not a good idea. Here is a minimal program with an infinite recursion:

```
function recurse()
    recurse()
end
```

In most programming environments, a program with infinite recursion does not really run forever. Julia reports an error message when the maximum recursion depth is reached

### Keyboard Input
when the user types something in the repl because the program is waiting for it

### Debugging 
When a syntax or runtime error occurs, the error message contains a lot of information, but it can be overwhelming. The most useful parts are usually:

-   What kind of error it was, and
    
-   Where it occurred.
    

Syntax errors are usually easy to find, but there are a few gotchas. In general, error messages indicate where the problem was discovered, but the actual error might be earlier in the code, sometimes on a previous line.

The same is true of runtime errors.


### floor division

An operator, denoted `÷` (in julia), that divides two numbers and rounds down (toward negative infinity) to an integer.

### modulus operator

An operator, denoted with a percent sign (%), that works on integers and returns the remainder when one number is divided by another.

### boolean expression

An expression whose value is either `true` or `false`.

### relational operator

One of the operators that compares its operands: `==`, `≠` (`!=`), `>`, `<`, `≥` (`>=`), and `≤` (`<=`).

### logical operator

One of the operators that combines boolean expressions: `&&` (and), `||` (or), and `!` (not).

### conditional statement

A statement that controls the flow of execution depending on some condition.

### condition

The boolean expression in a conditional statement that determines which branch runs.

### compound statement

A statement that consists of a header and a body. The body is terminated with the keyword `end`.

### branch

One of the alternative sequences of statements in a conditional statement.

### chained conditional

A conditional statement with a series of alternative branches.

### nested conditional

A conditional statement that appears in one of the branches of another conditional statement.

### return statement

A statement that causes a function to end immediately and return to the caller.

### recursion

The process of calling the function that is currently executing.

### base case

A conditional branch in a recursive function that does not make a recursive call.

### Infinite recursion

A recursion that doesn’t have a base case, or never reaches it. Eventually, an infinite recursion causes a runtime error.





### Return values of Fruitful functions
Calling the function generates a return value, which we usually assign to a variable or use as part of an expression

```
e = exp(1.0)
height = radius * sin(radians)
```

now the fruitful function
```
function area(radius)
    a = π * radius^2
    return a
end
```


in a fruitful function the `return` statement includes an expression. This statement means: “Return immediately from this function and use the following expression as a return value.”

Also, The value returned by a function is the value of the last expression evaluated, which, by default, is the last expression in the body of the function definition.
```
function area(radius)
    π * radius^2
end
```
On the other hand, _temporary variables_ like `a` and explicit `return` statements can make debugging easier.

As soon as a `return` statement runs, the function terminates without executing any subsequent statements. Code that appears after a `return` statement, or any other place the flow of execution can never reach, is called _dead code_.

In a fruitful function, it is a good idea to ensure that every possible path through the program hits a return statement.


### Incremental development

As you write larger functions, you might find yourself spending more time debugging.

To deal with increasingly complex programs, you might want to try a process called _incremental development_. The goal of incremental development is to avoid long debugging sessions by adding and testing only a small amount of code at a time.

When testing a function, it is useful to know the right answer.


Immediately you can write an outline of the function:

```
function distance(x₁, y₁, x₂, y₂)
    0.0
end
```


At this point we have confirmed that the function is syntactically correct, and we can start adding code to the body. A reasonable next step is to find the differences x2−x1 and y2−y1

. The next version stores those values in temporary variables and prints them with the `@show` macro.

```
function distance(x₁, y₁, x₂, y₂)
    dx = x₂ - x₁
    dy = y₂ - y₁
    @show dx dy
    0.0
end
```


f the function is working, it should display `dx = 3` and `dy = 4`. If so, we know that the function is getting the right arguments and performing the first computation correctly. If not, there are only a few lines to check.

Next we compute the sum of squares of `dx` and `dy`:

```
function distance(x₁, y₁, x₂, y₂)
    dx = x₂ - x₁
    dy = y₂ - y₁
    d² = dx^2 + dy^2
    @show d²
    0.0
end
```

Again, you would run the program at this stage and check the output (which should be 25). Superscript numbers are also available (**`\^2 TAB`**). Finally, you can use `sqrt` to compute and return the result:

```
function distance(x₁, y₁, x₂, y₂)
    dx = x₂ - x₁
    dy = y₂ - y₁
    d² = dx^2 + dy^2
    sqrt(d²)
end
```

If that works correctly, you are done. Otherwise, you might want to print the value of `sqrt(d²)` before the `return` statement.

The final version of the function doesn’t display anything when it runs; it only returns a value. The print statements we wrote are useful for debugging, but once you get the function working, you should remove them. Code like that is called _scaffolding_ because it is helpful for building the program but is not part of the final product.

When you start out, you should add only a line or two of code at a time. As you gain more experience, you might find yourself writing and debugging bigger chunks. Either way, incremental development can save you a lot of debugging time.

The key aspects of the process are:

1.  Start with a working program and make small incremental changes. At any point, if there is an error, you should have a good idea where it is.
    
2.  Use variables to hold intermediate values so you can display and check them.
    
3.  Once the program is working, you might want to remove some of the scaffolding or consolidate multiple statements into compound expressions, but only if it does not make the program difficult to read.


### Function composition
As you should expect by now, you can call one function from within another.


### Boolean Functions
Functions can return booleans, which is often convenient for hiding complicated tests inside functions. For example:

```
function isdivisible(x, y)
    if x % y == 0 ## test is remainder is 0
        return true
    else
        return false
    end
end
```


It is common to give boolean functions names that sound like yes/no questions; `isdivisible` returns either `true` or `false` to indicate whether `x` is divisible by `y`.

The result of the `==` operator is a boolean, so we can write the function more concisely by returning it directly:

```
function isdivisible(x, y)
    x % y == 0
end
```

Boolean functions are often used in conditional statements:

```
if isdivisible(x, y)
    println("x is divisible by y")
end
```


It might be tempting to write something like:

```
if isdivisible(x, y) == true
    println("x is divisible by y")
end
```

But the extra comparison with `true` is unnecessary (because isdivisible(x, y) already evaluates to true or false, and if true is enough, not needed a if true == true).

### Guardian pattern

```
function fact(n)
    if !(n isa Int64)
        error("Factorial is only defined for integers.")
    elseif n < 0
        error("Factorial is not defined for negative integers.")
    elseif n == 0
        return 1
    else
        return n * fact(n-1)
    end
end
```

This program demonstrates a pattern sometimes called a _guardian_. The first two conditionals act as guardians, protecting the code that follows from values that might cause an error. The guardians make it possible to prove the correctness of the code.


### Debugging
Breaking a large program into smaller functions creates natural checkpoints for debugging. If a function is not working, there are three possibilities to consider:

-   There is something wrong with the arguments the function is getting; a precondition is violated.
    
-   There is something wrong with the function; a postcondition is violated.
    
-   There is something wrong with the return value or the way it is being used.
    

To rule out the first possibility, you can add a print statement at the beginning of the function and display the values of the parameters (and maybe their types). Or you can write code that checks the preconditions explicitly.

If the parameters look good, add a print statement before each return statement and display the return value. If possible, check the result by hand. Consider calling the function with values that make it easy to check the result (as in [Incremental Development](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#incremental_development)).

If the function seems to be working, look at the function call to make sure the return value is being used correctly (or used at all!).

Adding print statements at the beginning and end of a function can help make the flow of execution more visible. For example, here is a version of `fact` with print statements:

```
function fact(n)
    space = " " ^ (4 * n)
    println(space, "factorial ", n)
    if n == 0
        println(space, "returning 1")
        return 1
    else
        recurse = fact(n-1)
        result = n * recurse
        println(space, "returning ", result)
        return result
    end
end
```


### temporary variable

A variable used to store an intermediate value in a complex calculation.

### dead code

Part of a program that can never run, often because it appears after a return statement.

### incremental development

A program development plan intended to avoid debugging by adding and testing only a small amount of code at a time.

### scaffolding

Code that is used during program development but is not part of the final version.

### guardian

A programming pattern that uses a conditional statement to check for and handle circumstances that might cause an error.



### Iteration

#### While loop
In a computer program, repetition is also called _iteration_.

More formally, here is the flow of execution for a `while` statement:

1.  Determine whether the condition is true or false.
    
2.  If false, exit the while statement and continue execution at the next statement.
    
3.  If the condition is true, run the body and then go back to step 1.
    

This type of flow is called a loop because the third step loops back around to the top.


The body of the loop should change the value of one or more variables so that the condition becomes false eventually and the loop terminates. Otherwise the loop will repeat forever, which is called an _infinite loop_.
```
function countdown(n)
    while n > 0
        print(n, " ")
        n = n - 1
    end
    println("Blastoff!")
end
```
Sometimes you don’t know it’s time to end a loop until you get half way through the body. In that case you can use the _break statement_ to jump out of the loop.

```
while true
    print("> ")
    line = readline()
    if line == "done"
        break
    end
    println(line)
end
println("Done!")
```

The break statement exits the loop. When a _continue statement_ is encountered inside a loop, control jumps to the beginning of the loop for the next iteration, skipping the execution of statements inside the body of the loop for the current iteration. For example:

```
for i in 1:10
    if i % 3 == 0
        continue
    end
    print(i, " ")
end
```

### Algotrithms
... an _algorithm_: it is a mechanical process for solving a category of problems...
One of the characteristics of algorithms is that they do not require any intelligence to carry out. They are mechanical processes where each step follows from the last according to a simple set of rules.

Executing algorithms is boring, but designing them is interesting, intellectually challenging, and a central part of computer science.

### Debugging
As you start writing bigger programs, you might find yourself spending more time debugging. More code means more chances to make an error and more places for bugs to hide.

One way to cut your debugging time is “debugging by bisection”. For example, if there are 100 lines in your program and you check them one at a time, it would take 100 steps.

Instead, try to break the problem in half. Look at the middle of the program, or near it, for an intermediate value you can check. Add a print statement (or something else that has a verifiable effect) and run the program.

If the mid-point check is incorrect, there must be a problem in the first half of the program. If it is correct, the problem is in the second half.

Every time you perform a check like this, you halve the number of lines you have to search. After six steps (which is fewer than 100), you would be down to one or two lines of code, at least in theory.

In practice it is not always clear what the “middle of the program” is and not always possible to check it. It doesn’t make sense to count lines and find the exact midpoint. Instead, think about places in the program where there might be errors and places where it is easy to put a check. Then choose a spot where you think the chances are about the same that the bug is before or after the check.


### Glossary
#### reassignment

Assigning a new value to a variable that already exists.

#### update

An assignment where the new value of the variable depends on the old.

#### initialization

An assignment that gives an initial value to a variable that will be updated.

#### increment

An update that increases the value of a variable (often by one).

#### decrement

An update that decreases the value of a variable.

#### iteration

Repeated execution of a set of statements using either a recursive function call or a loop.

#### while statement

Statement that allows iterations controlled by a condition.

#### break statement

Statement allowing to jump out of a loop.

#### continue statement

Statement inside a loop that jumps to the beginning of the loop for the next iteration.

#### infinite loop

A loop in which the terminating condition is never satisfied.

#### algorithm

A general process for solving a category of problems.






### Strings
Strings are not like integers, floats, and booleans. A string is a _sequence_ (of characters), which means it is an ordered collection of other values.


### Characters
English language speakers are familiar with characters such as the letters of the alphabet (A, B, C, …​), numerals, and common punctuation. These characters are standardized and mapped to integer values between 0 and 127 by the _ASCII standard_ (American Standard Code for Information Interchange).

The _Unicode standard_ tackles the complexities of what exactly a character is, and is generally accepted as the definitive standard addressing this problem. It provides a unique number for every character on a world-wide scale.



### Traversal (pattern of processing)
A lot of computations involve processing a string one character at a time. Often they start at the beginning, select each character in turn, do something to it, and continue until the end. This pattern of processing is called a _traversal_. One way to write a traversal is with a `while` loop:

```
index = firstindex(fruits)
while index <= sizeof(fruits)
    letter = fruits[index]
    println(letter)
    global index = nextind(fruits, index)
end
```



### String slices

A segment of a string is called a _slice_. Selecting a slice is similar to selecting a character:

```
julia> str = "Julius Caesar";

julia> str[1:6]
"Julius"
```

The operator `[n:m]` returns the part of the string from the `n`-th byte to the `m`-th byte. So the same caution is needed as for simple indexing.

The `end` keyword can be used to indicate the last byte of the string:

```
julia> str[8:end]
"Caesar"
```

If the first index is greater than the second the result is an _empty string_, represented by two quotation marks:

```
julia> str[8:7]
""
```

An empty string contains no characters and has length 0, but other than that, it is the same as any other string.

#### Strings are immutable. 


#### Glossary

#### sequence

An ordered collection of values where each value is identified by an integer index.

#### ASCII standard

A character encoding standard for electronic communication specifying 128 characters.

#### Unicode standard

A computing industry standard for the consistent encoding, representation, and handling of text expressed in most of the world’s writing systems.

#### index

An integer value used to select an item in a sequence, such as a character in a string. In Julia indices start from 1.


#### UTF-8 encoding
A variable width character encoding capable of encoding all 1112064 valid code points in Unicode using one to four 8-bit bytes.

#### traverse

To iterate through the items in a sequence, performing a similar operation on each.

#### slice

A part of a string specified by a range of indices.

#### empty string

A string with no characters and length 0, represented by two quotation marks.

#### immutable

The property of a sequence whose items cannot be changed.

#### string interpolation

The process of evaluating a string containing one or more placeholders, yielding a result in which the placeholders are replaced with their corresponding values.

#### search

A pattern of traversal that stops when it finds what it is looking for.

#### counter

A variable used to count something, usually initialized to zero and then incremented.




### Development plan: Reduction to a previously solved problem
This means that you recognize the problem you are working on as an instance of a solved problem and apply an existing solution. 

say we have this function
```
function usesonly(word, available)
    for letter in word
        if letter ∉ available
            return false
        end
    end
    true
end
```

and we want to achieve something with the following function
```
function usesall(word, required)
    for letter in required
        if letter ∉ word
            return false
        end
    end
    true
end
```
Using the development plan, we could rewrite the last function as
```
function usesall(word, required)
    usesonly(required, word)
end
```




### Debugging 

Testing programs is hard. The functions in this chapter are relatively easy to test because you can check the results by hand. Even so, it is somewhere between difficult and impossible to choose a set of words that test for all possible errors.

Taking `hasno_e` as an example, there are two obvious cases to check: words that have an `_e_` should return `false`, and words that don’t should return `true`. You should have no trouble coming up with one of each.

Within each case, there are some less obvious subcases. Among the words that have an “e”, you should test words with an “e” at the beginning, the end, and somewhere in the middle. You should test long words, short words, and very short words, like the empty string. The empty string is an example of a _special case_, which is one of the non-obvious cases where errors often lurk.

In addition to the test cases you generate, you can also test your program with a word list like `words.txt`. By scanning the output, you might be able to catch errors, but be careful: you might catch one kind of error (words that should not be included, but are) and not another (words that should be included, but aren’t).

In general, testing can help you find bugs, but it is not easy to generate a good set of test cases, and even if you do, you can’t be sure your program is correct. According to a legendary computer scientist:

> Program testing can be used to show the presence of bugs, but never to show their absence!
— Edsger W. Dijkstra


### Glossary

#### File stream
a value that represents an open file

#### Reduction to a previously solved problem
a way of solving a problem by expressing it as an instance of a previously solved problem

#### Special case
a test case that is atypical or non-obvious (and less likely to be handled correctly)





### 10. Arrays

#### An array is a sequence

Like a string, an _array_ is a sequence of values. In a string, the values are characters; in an array, they can be any type. The values in an array are called _elements_ or sometimes _items_.

There are several ways to create a new array; the simplest is to enclose the elements in square brackets (`[ ]`):

```
[10, 20, 30, 40]
["crunchy frog", "ram bladder", "lark vomit"]
```

The elements of an array don’t have to be the same type. The following array contains a string, a float, an integer, and another array:

```
["spam", 2.0, 5, [10, 20]]
```

An array within another array is _nested_.

An array that contains no elements is called an empty array; you can create one with empty brackets, `[]`.

As you might expect, you can assign array values to variables:

```
julia> cheeses = ["Cheddar", "Edam", "Gouda"];

julia> numbers = [42, 123];

julia> empty = [];

julia> print(cheeses, " ", numbers, " ", empty)
["Cheddar", "Edam", "Gouda"] [42, 123] Any[]
```

The function `typeof` can be used to find out the kind of the array:

```
julia> typeof(cheeses)
Array{String,1}
julia> typeof(numbers)
Array{Int64,1}
julia> typeof(empty)
Array{Any,1}
```

The kind of the array is specified between curly braces and is composed of a type and a number. The number indicates the dimensions. The array `empty` contains values of type `Any`., i.e. it can hold values of all types.

#### Arrays are mutable

The syntax for accessing the elements of an array is the same as for accessing the characters of a string—the bracket operator. The expression inside the brackets specifies the index. Remember that the indices start at 1:

```
julia> cheeses[1]
"Cheddar"
```

Unlike strings, arrays are _mutable_. When the bracket operator appears on the left side of an assignment, it identifies the element of the array that will be assigned:

```
julia> numbers[2] = 5
5
julia> print(numbers)
[42, 5]
```

Array indices work the same way as string indices (but without UTF-8 caveats):

-   Any integer expression can be used as an index.
    
-   If you try to read or write an element that does not exist, you get a `BoundsError`.
    
-   The keyword `end` points to the last index of the array.
    

The `∈` operator also works on arrays:

```
julia> "Edam" ∈ cheeses
true
julia> "Brie" in cheeses
false
```

#### Traversing an array

```
for cheese in cheeses
    println(cheese)
end
```
if you want to write or update the elements, you need the indices. A common way to do that is to use the built-in function `eachindex`:

```
for i in eachindex(numbers)
    numbers[i] = numbers[i] * 2
end
```

A `for` loop over an empty array never runs the body:

```
for x in []
    println("This can never happens.")
end
```

Although an array can contain another array, the nested array still counts as a single element. The length of this array is four:

```
["spam", 1, ["Brie", "Roquefort", "Camembert"], [1, 2, 3]]
```

#### Array slices
The slice operator also works on arrays:

```
julia> t = ['a', 'b', 'c', 'd', 'e', 'f'];

julia> print(t[1:3])
['a', 'b', 'c']
julia> print(t[3:end])
['c', 'd', 'e', 'f']
```

The slice operator `[:]`, makes a copy of the whole array:

```
julia> print(t[:])
['a', 'b', 'c', 'd', 'e', 'f']
```

Since arrays are mutable, it is often useful to make a copy before performing operations that modify arrays.

A slice operator on the left side of an assignment can update multiple elements:

```
julia> t[2:3] = ['x', 'y'];

julia> print(t)
['a', 'x', 'y', 'd', 'e', 'f']
```

#### Array library
Julia provides functions that operate on arrays. For example, `push!` adds a new element to the end of an array:

```
julia> t = ['a', 'b', 'c'];

julia> push!(t, 'd');

julia> print(t)
['a', 'b', 'c', 'd']
```

`append!` add the elements of the second array to the end of the first:

```
julia> t1 = ['a', 'b', 'c'];

julia> t2 = ['d', 'e'];

julia> append!(t1, t2);

julia> print(t1)
['a', 'b', 'c', 'd', 'e']
```

This example leaves `t2` unmodified (but not t1 because of the `!`).

`sort!` arranges the elements of the array from low to high:

```
julia> t = ['d', 'c', 'e', 'b', 'a'];

julia> sort!(t);

julia> print(t)
['a', 'b', 'c', 'd', 'e']
```

As a style convention in Julia, `!` is appended to names of functions that modify their arguments.


#### Map, Filter and Reduce
To add up all the numbers in an array, you can use a loop like this:

```
function addall(t)
    total = 0
    for x in t
        total += x
    end
    total
end
```

`total` is initialized to 0. Each time through the loop, `+=` gets one element from the array. The `+=` operator provides a short way to update a variable. This **_augmented assignment statement_**,

```
total += x
```

is equivalent to

```
total = total + x
```


#### Accumulator
As the loop runs, `total` accumulates the sum of the elements; a variable used this way is sometimes called an _accumulator_.

Adding up the elements of an array is such a common operation that Julia provides it as a built-in function, `sum`:

```
julia> t = [1, 2, 3, 4];

julia> sum(t)
10
```


#### Reduce operation
An operation like this that combines a sequence of elements into a single value is sometimes called a _reduce operation_.



#### Map

```
function capitalizeall(t)
    res = []
    for s in t
        push!(res, uppercase(s))
    end
    res
end
```

An operation like `capitalizeall` is sometimes called a _map_ because it “maps” a function (in this case `uppercase`) onto each of the elements in a sequence.


#### Filter
Another common operation is to select some of the elements from an array and return a subarray. For example, the following function takes an array of strings and returns an array that contains only the uppercase strings:

```
function onlyupper(t)
    res = []
    for s in t
        if s == uppercase(s)
            push!(res, s)
        end
    end
    res
end
```

An operation like `onlyupper` is called a _filter_ because it selects some of the elements and filters out the others.

Most common array operations can be expressed as a combination of map, filter and reduce.


### Dot Syntax
For every binary operator like `^`, there is a corresponding _dot operator_ `.^` that is automatically defined to perform `^` element-by-element on arrays. For example, `[1, 2, 3] ^ 3` is not defined, but `[1, 2, 3] .^ 3` is defined as computing the elementwise result `[1^3, 2^3, 3^3]`:

```
julia> print([1, 2, 3] .^ 3)
[1, 8, 27]
```

Any Julia function `f` can be applied elementwise to any array with the _dot syntax_. For example to capitalize an array of strings, we don’t need an explicit loop:

```
julia> t = uppercase.(["abc", "def", "ghi"]);

julia> print(t)
["ABC", "DEF", "GHI"]
```

This is an elegant way to create a map. The function `capitalizeall` can be implemented by a one-liner:

```
function capitalizeall(t)
    uppercase.(t)
end
```


#### Deleting (Inserting) elements
There are several ways to delete elements from an array. If you know the index of the element you want, you can use `splice!`:

```
julia> t = ['a', 'b', 'c'];

julia> splice!(t, 2)
'b': ASCII/Unicode U+0062 (category Ll: Letter, lowercase)
julia> print(t)
['a', 'c']
```

`splice!` modifies the array and returns the element that was removed.

`pop!` deletes and returns the last element:

```
julia> t = ['a', 'b', 'c'];

julia> pop!(t)
'c': ASCII/Unicode U+0063 (category Ll: Letter, lowercase)
julia> print(t)
['a', 'b']
```

`popfirst!` deletes and returns the first element:

```
julia> t = ['a', 'b', 'c'];

julia> popfirst!(t)
'a': ASCII/Unicode U+0061 (category Ll: Letter, lowercase)
julia> print(t)
['b', 'c']
```

The functions `pushfirst!` and `push!` insert an element at the beginning, respectively at the end of the array.

If you don’t need the removed value, you can use the function `deleteat!`:

```
julia> t = ['a', 'b', 'c'];

julia> print(deleteat!(t, 2))
['a', 'c']
```

The function `insert!` inserts an element at a given index:

```
julia> t = ['a', 'b', 'c'];

julia> print(insert!(t, 2, 'x'))
['a', 'x', 'b', 'c']
```


#### Arrays and strings

A string is a sequence of characters and an array is a sequence of values, but an array of characters is not the same as a string. To convert from a string to an array of characters, you can use the function `collect`:

```
julia> t = collect("spam");

julia> print(t)
['s', 'p', 'a', 'm']
```

The `collect` function breaks a string or another sequence into individual elements.

If you want to break a string into words, you can use the `split` function:

```
julia> t = split("pining for the fjords");

julia> print(t)
SubString{String}["pining", "for", "the", "fjords"]
```

An _optional argument_ called a _delimiter_ specifies which characters to use as word boundaries. The following example uses a hyphen as a delimiter:

```
julia> t = split("spam-spam-spam", '-');

julia> print(t)
SubString{String}["spam", "spam", "spam"]
```

`join` is the inverse of `split`. It takes an array of strings and concatenates the elements:

```
julia> t = ["pining", "for", "the", "fjords"];

julia> s = join(t, ' ')
"pining for the fjords"
```

In this case the delimiter is a space character. To concatenate strings without spaces, you don’t specify a delimiter.



#### Objects and Values
An **object is something a variable can refer to**.


![[Pasted image 20220805110654.png]]


In this case we would say that the two arrays are _equivalent_, because they have the same elements, but not _identical_, because they are not the same object. If two objects are identical, they are also equivalent, but if they are equivalent, they are not necessarily identical.

To be precise an object has a value. If you evaluate `[1, 2, 3]`, you get an array object whose value is a sequence of integers. If another array has the same elements, we say it has the same value, but it is not the same object.




### Aliasing

If `a` refers to an object and you assign `b = a`, then both variables refer to the same object:

```
julia> a = [1, 2, 3];

julia> b = a;

julia> b ≡ a
true
```


![[Pasted image 20220805110855.png]]


The association of a variable with an object is called a _reference_. In this example, there are two references to the same object.

An object with more than one reference has more than one name, so we say that the object is _aliased_.

If the aliased object is mutable, changes made with one alias affect the other:

```
julia> b[1] = 42
42
julia> print(a)
[42, 2, 3]
```
WARNING. 
Although this behavior can be useful, it is error-prone. In general, it is safer to avoid aliasing when you are working with mutable objects.

For immutable objects like strings, aliasing is not as much of a problem. In this example:

```
a = "banana"
b = "banana"
```

It almost never makes a difference whether `a` and `b` refer to the same string or not.


#### Array arguments



### Debugging

Careless use of arrays (and other mutable objects) can lead to long hours of debugging. Here are some common pitfalls and ways to avoid them:

-   Most array functions modify the argument. This is the opposite of the string functions, which return a new string and leave the original alone.
    
    If you are used to writing string code like this:
    
    ```
    new_word = strip(word)
    ```
    
    It is tempting to write array code like this:
    
    ```
    t2 = sort!(t1)
    ```
    
    Because `sort!` returns the modified original array `t1`, `t2` is an alias of `t1`.
    
    Tip.
    Before using array functions and operators, you should read the documentation carefully and then test them in interactive mode.


-   Pick an idiom and stick with it.
    
    Part of the problem with arrays is that there are too many ways to do things. For example, to remove an element from an array, you can use `pop!`, `popfirst!`, `delete_at`, or even a slice assignment. To add an element, you can use `push!`, `pushfirst!`, `insert!` or `vcat`. Assuming that `t` is an array and `x` is an array element, these are correct:
    
    ```
    insert!(t, 4, x)
    push!(t, x)
    append!(t, [x])
    ```
    
    And these are wrong:
    
    ```
    insert!(t, 4, [x])         # WRONG!
    push!(t, [x])              # WRONG!
    vcat(t, [x])               # WRONG!
    ```
    
-   Make copies to avoid aliasing.
    
    If you want to use a function like `sort!` that modifies the argument, but you need to keep the original array as well, you can make a copy:
    
    ```
    julia> t = [3, 1, 2];
    
    julia> t2 = t[:]; # t2 = copy(t)
    
    julia> sort!(t2);
    
    julia> print(t)
    [3, 1, 2]
    julia> print(t2)
    [1, 2, 3]
    ```
    
    In this example you could also use the built-in function `sort`, which returns a new, sorted array and leaves the original alone:
    
    ```
    julia> t2 = sort(t);
    
    julia> println(t)
    [3, 1, 2]
    julia> println(t2)
    [1, 2, 3]
    ```
    

### Glossary

### array

A sequence of values.

### element

One of the values in an array (or other sequence), also called items.

### nested array

An array that is an element of another array.

### accumulator

A variable used in a loop to add up or accumulate a result.

### augmented assignment

A statement that updates the value of a variable using an operator like `=`.

### dot operator

Binary operator that is applied element-by-element to arrays.

### dot syntax

Syntax used to apply a function elementwise to any array.

### reduce operation

A processing pattern that traverses a sequence and accumulates the elements into a single result.

### map

A processing pattern that traverses a sequence and performs an operation on each element.

### filter

A processing pattern that traverses a sequence and selects the elements that satisfy some criterion.

### object

Something a variable can refer to. An object has a type and a value.


### equivalent

Having the same value.


### identical

Being the same object (which implies equivalence).

### reference

The association between a variable and its value.

### aliasing

A circumstance where two or more variables refer to the same object.

### optional arguments

arguments that are not required.

### delimiter

A character or string used to indicate where a string should be split.





### 11. Dictionaries
A _dictionary_ is like an array, but more general. In an array, the indices have to be integers; in a dictionary they can be (almost) any type.

A dictionary contains a collection of indices, which are called _keys_, and a collection of values. Each key is associated with a single value. The association of a key and a value is called a _key-value pair_ or sometimes an item.

In mathematical language, a dictionary represents a _mapping_ from keys to values, so you can also say that each key “maps to” a value.


Warning
The order of the key-value pairs might not be the same. If you type the same example on your computer, you might get a different result. In general, the order of items in a dictionary is unpredictable.

But that’s not a problem because the elements of a dictionary are never indexed with integer indices. Instead, you use the keys to look up the corresponding values:

```
julia> eng2sp["two"]
"dos"
```

The key "two" always maps to the value "dos" so the order of the items doesn’t matter.




### Implementation
An _implementation_ is a way of performing a computation; some implementations are better than others.


### Lookup
Given a dictionary `d` and a key `k`, it is easy to find the corresponding value `v = d[k]`. This operation is called a _lookup_.

### Reverse lookup
But what if you have `v` and you want to find `k`? You have two problems: first, there might be more than one key that maps to the value `v`. Depending on the application, you might be able to pick one, or you might have to make an array that contains all of them. Second, there is no simple syntax to do a _reverse lookup_; you have to search.
Julia provides an optimized way to do a reverse lookup: `findall(isequal(3), h)`.

Warning.
A reverse lookup is much slower than a forward lookup; if you have to do it often, or if the dictionary gets big, the performance of your program will suffer.


### Dictionaries and Arrays

Arrays can appear as values in a dictionary.

Singleton: an array that contains a single element


Note: I mentioned earlier that a dictionary is implemented using a hash table and that means that the keys have to be _hashable_.
A **_hash_** is a function that takes a value (of any kind) and returns an integer. Dictionaries use these integers, called hash values, to store and look up key-value pairs.


### Memo
A previously computed value that is stored for later use is called a _memo_. Here is a “memoized” version of fibonacci:

```
known = Dict(0=>0, 1=>1)

function fibonacci(n)
    if n ∈ keys(known)
        return known[n]
    end
    res = fibonacci(n-1) + fibonacci(n-2)
    known[n] = res
    res
end
```


### Global variables
In the previous example, known is created outside the function, so it belongs to the special frame called `Main`. Variables in `Main` are sometimes called _global_ because they can be accessed from any function. Unlike local variables, which disappear when their function ends, global variables persist from one function call to the next.

The _global statement_ tells the interpreter something like, “In this function, when I say `been_called`, I mean the global variable; don’t create a local one.”

```
been_called = false

function example2()
    global been_called
    been_called = true
end
```


**Warning**. Global variables can be useful, but if you have a lot of them, and you modify them frequently, they can make programs hard to debug and perform badly.


### Debugging (11)


As you work with bigger datasets it can become unwieldy to debug by printing and checking the output by hand. Here are some suggestions for debugging large datasets:

-   Scale down the input:
    
    If possible, reduce the size of the dataset. For example if the program reads a text file, start with just the first 10 lines, or with the smallest example you can find which errors. You sould not edit the files themselves, but rather modify the program so it reads only the first n
    

lines.

If there is an error, you can reduce n

-   to the smallest value that manifests the error, and then increase it gradually as you find and correct errors.
    
-   Check summaries and types:
    
    Instead of printing and checking the entire dataset, consider printing summaries of the data: for example, the number of items in a dictionary or the total of an array of numbers.
    
    A common cause of runtime errors is a value that is not the right type. For debugging this kind of error, it is often enough to print the type of a value.
    
-   Write self-checks:
    
    Sometimes you can write code to check for errors automatically. For example, if you are computing the average of an array of numbers, you could check that the result is not greater than the largest element in the array or less than the smallest. This is called a “sanity check”.
    
    Another kind of check compares the results of two different computations to see if they are consistent. This is called a “consistency check”.
    
-   Format the output:
    
    Formatting debugging output can make it easier to spot an error. We saw an example in [Debugging](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#deb06).
    
    Again, time you spend building scaffolding can reduce the time you spend debugging.


### Glossary (11)
#### Mapping
a relationship in which each element of one set corresponds to an element of another set. 

#### Dictionary
A mapping from keys to their corresponding values

#### Key-value pair
The representation of the mapping from a key to a value

#### Item
In a dictionary, another name for a key-value pair

#### key
An object that appears in a dictionary as the first part of a key-value pair

#### Value
An object that appears in a dictionary as the second part of a key-value pair. This is more specific than our previours use of the word "value"

#### Implementation
a way of performing a computation

#### Hash table
the algorithm used to implement julia dictionaries. 

#### hash function
a funcion used by the hash table to compute the location for a key. 

#### Lookup
a dictionary operation that takes a key and finds it's value

#### Reverse lookup
a dictionary operation that takes a value and finds one or more keys that map to that value

#### Singleton
an array (or other sequence) with a single element

#### call graph

A diagram that shows every frame created during the execution of a program, with an arrow from each caller to each callee.

#### memo

A computed value stored to avoid unnecessary future computation.

#### global variable

A variable defined outside a function. Global variables can be accessed from any function.

#### global statement

A statement that declares a variable name global.

#### flag

A boolean variable used to indicate whether a condition is true.

#### declaration

A statement like `global` that tells the interpreter something about a variable.

#### constant global variable

A global variable that can not be reassigned.




### 12. Tuples
This chapter presents one more built-in type, the tuple, and then shows how arrays, dictionaries, and tuples work together. I also present a useful feature for variable-length argument arrays, the gather and scatter operators.

#### Tuples are immutable

A tuple is a sequence of values. The values can be of any type, and they are indexed by integers, so in that respect tuples are a lot like arrays. The important difference is that tuples are immutable and that each element can have its own type.

Syntactically, a tuple is a comma-separated list of values:

```
julia> t = 'a', 'b', 'c', 'd', 'e'
('a', 'b', 'c', 'd', 'e')
```

Although it is not necessary, it is common to enclose tuples in parentheses:

```
julia> t = ('a', 'b', 'c', 'd', 'e')
('a', 'b', 'c', 'd', 'e')
```

To create a tuple with a single element, you have to include a final comma:

```
julia> t1 = ('a',)
('a',)
julia> typeof(t1)
Tuple{Char}
```

**Warning**. A value in parentheses without comma is not a tuple:

```
julia> t2 = ('a')
'a': ASCII/Unicode U+0061 (category Ll: Letter, lowercase)
julia> typeof(t2)
Char
```

Most array operators also work on tuples. The bracket operator indexes an element:

If you try to modify one of the elements of the tuple, you get an error:

```
julia> t[1] = 'A'
ERROR: MethodError: no method matching setindex!(::NTuple{5,Char}, ::Char, ::Int64)
```
Because tuples are immutable, you can’t modify the elements.


... tuple assignment is more elegant:

```
a, b = b, a
```

The left side is a tuple of variables; the right side is a tuple of expressions. Each value is assigned to its respective variable. All the expressions on the right side are evaluated before any of the assignments.

The number of variables on the left has to be fewer than the number of values on the right:

```
julia> (a, b) = (1, 2, 3)
(1, 2, 3)
julia> a, b, c = 1, 2
ERROR: BoundsError: attempt to access (1, 2)
  at index [3]
```

More generally, the right side can be any kind of sequence (string, array or tuple). For example, to split an email address into a user name and a domain, you could write:

```
julia> addr = "julius.caesar@rome"
"julius.caesar@rome"
julia> uname, domain = split(addr, '@');
```

The return value from `split` is an array with two elements; the first element is assigned to `uname`, the second to `domain`.

```
julia> uname
"julius.caesar"
julia> domain
"rome"
```



#### Tuples as Return Values
Strictly speaking, a function can only return one value, but if the value is a tuple, the effect is the same as returning multiple values. For example, if you want to divide two integers and compute the quotient and remainder, it is inefficient to compute `x ÷ y` and then `x % y`. It is better to compute them both at the same time.


The built-in function `divrem` takes two arguments and returns a tuple of two values, the quotient and remainder. You can store the result as a tuple:

```
julia> t = divrem(7, 3)
(2, 1)
```

Or use tuple assignment to store the elements separately:

```
julia> q, r = divrem(7, 3);

julia> @show q r;
q = 2
r = 1
```

Here is an example of a function that returns a tuple:

```
function minmax(t)
    minimum(t), maximum(t)
end
```

### Variable-length Argument Tuples
Functions can take a variable number of arguments. A parameter name that ends with `...` _gathers_ arguments into a tuple. For example, `printall` takes any number of arguments and prints them:

```
function printall(args...)
    println(args)
end
```

The gather parameter can have any name you like, but `args` is conventional. Here’s how the function works:

```
julia> printall(1, 2.0, '3')
(1, 2.0, '3')
```


The complement of gather is _scatter_. If you have a sequence of values and you want to pass it to a function as multiple arguments, you can use the `...` operator. For example, `divrem` takes exactly two arguments; it doesn’t work with a tuple:

```
julia> t = (7, 3);

julia> divrem(t)
ERROR: MethodError: no method matching divrem(::Tuple{Int64,Int64})
```

But if you scatter the tuple, it works:

```
julia> divrem(t...)
(2, 1)
```

#### Arrays and Tuples

`zip` is a built-in function that takes two or more sequences and returns a collection of tuples where each tuple contains one element from each sequence. The name of the function refers to a zipper, which joins and interleaves two rows of teeth.

This example zips a string and an array:

```
julia> s = "abc";

julia> t = [1, 2, 3];

julia> zip(s, t)
Base.Iterators.Zip{Tuple{String,Array{Int64,1}}}(("abc", [1, 2, 3]))
```

The result is a _zip object_ that knows how to iterate through the pairs. The most common use of `zip` is in a `for` loop:

```
julia> for pair in zip(s, t)
           println(pair)
       end
('a', 1)
('b', 2)
('c', 3)
```


**Iterators**. A zip object is a kind of _iterator_, which is any object that iterates through a sequence. Iterators are similar to arrays in some ways, but unlike arrays, you can’t use an index to select an element from an iterator.

If you want to use array operators and functions, you can use a zip object to make an array:

```
julia> collect(zip(s, t))
3-element Array{Tuple{Char,Int64},1}:
 ('a', 1)
 ('b', 2)
 ('c', 3)
```

The result is an array of tuples; in this example, each tuple contains a character from the string and the corresponding element from the array.

If the sequences are not the same length, the result has the length of the shorter one.

```
julia> collect(zip("Anne", "Elk"))
3-element Array{Tuple{Char,Char},1}:
 ('A', 'E')
 ('n', 'l')
 ('n', 'k')
```

You can use tuple assignment in a `for` loop to traverse an array of tuples:

```
julia> t = [('a', 1), ('b', 2), ('c', 3)];

julia> for (letter, number) in t
           println(number, " ", letter)
       end
1 a
2 b
3 c
```

Each time through the loop, Julia selects the next tuple in the array and assigns the elements to letter and number. The parentheses around `(letter, number)` are compulsory.

If you combine `zip`, `for` and tuple assignment, you get a useful idiom for traversing two (or more) sequences at the same time. For example, `hasmatch` takes two sequences, `t1` and `t2`, and returns `true` if there is an index `i` such that `t1[i] == t2[i]`:

```
function hasmatch(t1, t2)
    for (x, y) in zip(t1, t2)
        if x == y
            return true
        end
    end
    false
end
```

If you need to traverse the elements of a sequence and their indices, you can use the built-in function `enumerate`:

```
julia> for (index, element) in enumerate("abc")
           println(index, " ", element)
       end
1 a
2 b
3 c
```

The result from `enumerate` is an enumerate object, which iterates a sequence of pairs; each pair contains an index (starting from 1) and an element from the given sequence.


#### Dictionaries and Tuples
Dictionaries can be used as iterators that iterate the key-value pairs. You can use it in a `for` loop like this:

```
julia> d = Dict('a'=>1, 'b'=>2, 'c'=>3);

julia> for (key, value) in d
           println(key, " ", value)
       end
a 1
c 3
b 2
```

As you should expect from a dictionary, the items are in no particular order.

Going in the other direction, you can use an array of tuples to initialize a new dictionary:

```
julia> t = [('a', 1), ('c', 3), ('b', 2)];

julia> d = Dict(t)
Dict{Char,Int64} with 3 entries:
  'a' => 1
  'c' => 3
  'b' => 2
```

Combining `Dict` with `zip` yields a concise way to create a dictionary:

```
julia> d = Dict(zip("abc", 1:3))
Dict{Char,Int64} with 3 entries:
  'a' => 1
  'c' => 3
  'b' => 2
```

It is common to use tuples as keys in dictionaries. For example, a telephone directory might map from last-name, first-name pairs to telephone numbers. Assuming that we have defined `last`, `first` and `number`, we could write:

```
directory[last, first] = number
```

The expression in brackets is a tuple. We could use tuple assignment to traverse this dictionary.

```
for ((last, first), number) in directory
    println(first, " ", last, " ", number)
end
```

This loop traverses the key-value pairs in `directory`, which are tuples. It assigns the elements of the key in each tuple to `last` and `first`, and the value to `number`, then prints the name and corresponding telephone number.


#### Sequences of Sequences


I have focused on arrays of tuples, but almost all of the examples in this chapter also work with arrays of arrays, tuples of tuples, and tuples of arrays. To avoid enumerating the possible combinations, it is sometimes easier to talk about sequences of sequences.

In many contexts, the different kinds of sequences (strings, arrays and tuples) can be used interchangeably. So how should you choose one over the others?

To start with the obvious, strings are more limited than other sequences because the elements have to be characters. They are also immutable. If you need the ability to change the characters in a string (as opposed to creating a new string), you might want to use an array of characters instead.

Arrays are more common than tuples, mostly because they are mutable. But there are a few cases where you might prefer tuples:

-   In some contexts, like a return statement, it is syntactically simpler to create a tuple than an array.
    
-   If you are passing a sequence as an argument to a function, using tuples reduces the potential for unexpected behavior due to aliasing.
    
-   For performance reasons. The compiler can specialize on the type.

Because tuples are immutable, they don’t provide functions like `sort!` and `reverse!`, which modify existing arrays. But Julia provides the built-in function `sort`, which takes an array and returns a new array with the same elements in sorted order, and `reverse`, which takes any sequence and returns a sequence of the same type in reverse order.


#### Debugging (12)
Arrays, dictionaries and tuples are examples of _data structures_; in this lecture we are starting to see compound data structures, like arrays of tuples, or dictionaries that contain tuples as keys and arrays as values. Compound data structures are useful, but they are prone to what I call _shape errors_; that is, errors caused when a data structure has the wrong type, size, or structure. For example, if you are expecting an array with one integer and I give you a plain old integer (not in an array), it won’t work.

Julia allows to attach a type to elements of a sequence. How this is done is detailed in [Multiple Dispatch](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#chap17). Specifying the type eliminates a lot of shape errors.

#### Glossary (12)
#### tuple

An immutable sequence of elements where every element can have its own type.

#### tuple assignment

An assignment with a sequence on the right side and a tuple of variables on the left. The right side is evaluated and then its elements are assigned to the variables on the left.

#### gather

The operation of assembling a variable-length argument tuple.

#### scatter

The operation of treating a sequence as a list of arguments.

#### zip object

The result of calling a built-in function `zip`; an object that iterates through a sequence of tuples.

#### iterator

An object that can iterate through a sequence, but which does not provide array operators and functions.

#### data structure

A collection of related values, often organized in array, dictionaries, tuples, etc.

#### shape error

An error caused because a value has the wrong shape; that is, the wrong type or size.



#### 13. How to choose between data structures 

How should you choose? The first step is to think about the operations you will need to implement for each data structure. For the prefixes, we need to be able to remove words from the beginning and add to the end. For example, if the current prefix is “Half a”, and the next word is “bee”, you need to be able to form the next prefix, “a bee”.

Your first choice might be an array, since it is easy to add and remove elements.

For the collection of suffixes, the operations we need to perform include adding a new suffix (or increasing the frequency of an existing one), and choosing a random suffix.

Adding a new suffix is equally easy for the array implementation or the histogram. Choosing a random element from an array is easy; choosing from a histogram is harder to do efficiently (see [Exercise 13-7](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#ex13-7)).

So far we have been talking mostly about ease of implementation, but there are other factors to consider in choosing data structures. One is run time. Sometimes there is a theoretical reason to expect one data structure to be faster than other; for example, I mentioned that the `in` operator is faster for dictionaries than for arrays, at least when the number of elements is large.

But often you don’t know ahead of time which implementation will be faster. One option is to implement both of them and see which is better. This approach is called _benchmarking_. A practical alternative is to choose the data structure that is easiest to implement, and then see if it is fast enough for the intended application. If so, there is no need to go on. If not, there are tools, like the `Profile` module, that can identify the places in a program that take the most time.

The other factor to consider is storage space. For example, using a histogram for the collection of suffixes might take less space because you only have to store each word once, no matter how many times it appears in the text. In some cases, saving space can also make your program run faster, and in the extreme, your program might not run at all if you run out of memory. But for many applications, space is a secondary consideration after run time.

One final thought: in this discussion, I have implied that we should use one data structure for both analysis and generation. But since these are separate phases, it would also be possible to use one structure for analysis and then convert to another structure for generation. This would be a net win if the time saved during generation exceeded the time spent in conversion.



#### Debugging (13)
When you are debugging a program, and especially if you are working on a hard bug, there are five things to try:

Reading

Examine your code, read it back to yourself, and check that it says what you meant to say.

Running

Experiment by making changes and running different versions. Often if you display the right thing at the right place in the program, the problem becomes obvious, but sometimes you have to build scaffolding.

Ruminating

Take some time to think! What kind of error is it: syntax, runtime, or semantic? What information can you get from the error messages, or from the output of the program? What kind of error could cause the problem you’re seeing? What did you change last, before the problem appeared?

Rubberducking

If you explain the problem to someone else, you sometimes find the answer before you finish asking the question. Often you don’t need the other person; you could just talk to a rubber duck. And that’s the origin of the well-known strategy called rubber duck debugging. I am not making this up; see [https://en.wikipedia.org/wiki/Rubber_duck_debugging](https://en.wikipedia.org/wiki/Rubber_duck_debugging).

Retreating

At some point, the best thing to do is back off, undoing recent changes, until you get back to a program that works and that you understand. Then you can start rebuilding.

Beginning programmers sometimes get stuck on one of these activities and forget the others. Each activity comes with its own failure mode.

For example, reading your code might help if the problem is a typographical error, but not if the problem is a conceptual misunderstanding. If you don’t understand what your program does, you can read it 100 times and never see the error, because the error is in your head.

Running experiments can help, especially if you run small, simple tests. But if you run experiments without thinking or reading your code, you might fall into a pattern I call “random walk programming”, which is the process of making random changes until the program does the right thing. Needless to say, random walk programming can take a long time.

You have to take time to think. Debugging is like an experimental science. You should have at least one hypothesis about what the problem is. If there are two or more possibilities, try to think of a test that would eliminate one of them.

But even the best debugging techniques will fail if there are too many errors, or if the code you are trying to fix is too big and complicated. Sometimes the best option is to retreat, simplifying the program until you get to something that works and that you understand.

Beginning programmers are often reluctant to retreat because they can’t stand to delete a line of code (even if it’s wrong). If it makes you feel better, copy your program into another file before you start stripping it down. Then you can copy the pieces back one at a time.

Finding a hard bug requires reading, running, ruminating, and sometimes retreating. If you get stuck on one of these activities, try the others.


#### Glossary (13)

#### deterministic

Pertaining to a program that does the same thing each time it runs, given the same inputs.

#### pseudorandom

Pertaining to a sequence of numbers that appears to be random, but is generated by a deterministic program.

#### default value

The value given to an optional parameter if no argument is provided.

#### override

To replace a default value with an argument.

#### benchmarking

The process of choosing between data structures by implementing alternatives and testing them on a sample of the possible inputs.

#### rubber duck debugging

Debugging by explaining your problem to an inanimate object such as a rubber duck. Articulating the problem can help you solve it, even if the rubber duck doesn’t know Julia.



### 14. Files

#### Persistence

Most of the programs we have seen so far are transient in the sense that they run for a short time and produce some output, but when they end, their data disappears. If you run the program again, it starts with a clean slate.

Other programs are _persistent_: they run for a long time (or all the time); they keep at least some of their data in permanent storage (a hard drive, for example); and if they shut down and restart, they pick up where they left off.

Examples of persistent programs are operating systems, which run pretty much whenever a computer is on, and web servers, which run all the time, waiting for requests to come in on the network.

One of the simplest ways for programs to maintain their data is by reading and writing _text files_. We have already seen programs that read text files; in this chapter we will see programs that write them.

An alternative is to store the state of the program in a database. In this chapter I will also present how to use a simple database.


A text file is a sequence of characters stored on a permanent medium like a hard drive, or flash memory. We saw how to open and read a file in [Reading Word Lists](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#reading_word_lists).


#### Filenames and Paths
Files are organized into _directories_ (also called “folders”). Every running program has a “current directory”, which is the default directory for most operations. For example, when you open a file for reading, Julia looks for it in the current directory.

A string like `"/home/ben"` that identifies a file or directory is called a _path_.

A simple filename, like `memo.txt` is also considered a path, but it is a _relative path_ because it relates to the current directory. If the current directory is `/home/ben`, the filename `memo.txt` would refer to `/home/ben/memo.txt`.

A path that begins with `/` does not depend on the current directory; it is called an _absolute path_. To find the absolute path to a file, you can use `abspath`:

```
julia> abspath("memo.txt")
"/home/ben/memo.txt"
```


#### Catching Exceptions

A lot of things can go wrong when you try to read and write files. If you try to open a file that doesn’t exist, you get a `SystemError`:

```
julia> fin = open("bad_file")
ERROR: SystemError: opening file "bad_file": No such file or directory
```

If you don’t have permission to access a file:

```
julia> fout = open("/etc/passwd", "w")
ERROR: SystemError: opening file "/etc/passwd": Permission denied
```


To avoid these errors, you could use functions like `ispath` and `isfile`, but it would take a lot of time and code to check all the possibilities.

It is easier to go ahead and try—and deal with problems if they happen—which is exactly what the `try` statement does. The syntax is similar to an `if` statement:

```
try
    fin = open("bad_file.txt")
catch exc
    println("Something went wrong: $exc")
end
```
Julia starts by executing the `try` clause. If all goes well, it skips the `catch` clause and proceeds. If an exception occurs, it jumps out of the `try` clause and runs the `catch` clause.

Handling an exception with a `try` statement is called _catching_ an exception. In this example, the except clause prints an error message that is not very helpful. In general, catching an exception gives you a chance to fix the problem, or try again, or at least end the program gracefully.


In code that performs state changes or uses resources like files, there is typically clean-up work (such as closing files) that needs to be done when the code is finished. Exceptions potentially complicate this task, since they can cause a block of code to exit before reaching its normal end. The `finally` keyword provides a way to run some code when a given block of code exits, regardless of how it exits:

```
f = open("output.txt")
try
    line = readline(f)
    println(line)
finally
    close(f)
end
```

The function `close` will always be executed.




#### Databases
A _database_ is a file that is organized for storing data. Many databases are organized like a dictionary in the sense that they map from keys to values. The biggest difference between a database and a dictionary is that the database is on disk (or other permanent storage), so it persists after the program ends.


#### Command Objects

Most operating systems provide a command-line interface, also known as a _shell_. Shells usually provide commands to navigate the file system and launch applications. For example, in Unix you can change directories with `cd`, display the contents of a directory with `ls`, and launch a web browser by typing (for example) `firefox`.

Any program that you can launch from the shell can also be launched from Julia using a _command object_:

```
julia> cmd = `echo hello`
```

Backticks are used to delimit the command.

The function `run` executes the command:

```
julia> run(cmd);
hello
```

#### Modules

Julia introduces modules to create separate variable workspace, i.e. new global scopes.


A module starts with the keyword `module` and ends with `end`. Naming conflicts are avoided between your own top-level definitions and those found in somebody else’s code. `import` allows to control which names from other modules are visible and `export` specifies which of your names are public, i.e. can be used outside the module without being prefixed with the name of the module.

```
module LineCount
    export linecount

    function linecount(filename)
        count = 0
        for line in eachline(filename)
            count += 1
        end
        count
    end
end
```

The module `LineCount` object provides `linecount`:

```
julia> using LineCount

julia> linecount("wc.jl")
11
```



#### Debugging (14)
When you are reading and writing files, you might run into problems with whitespace. These errors can be hard to debug because spaces, tabs and newlines are normally invisible:

```
julia> s = "1 2\t 3\n 4";

julia> println(s)
1 2     3
 4
```

The built-in functions `repr` or `dump` can help. It takes any object as an argument and returns a string representation of the object.

```
julia> repr(s)
"\"1 2\\t 3\\n 4\""
julia> dump(s)
String "1 2\t 3\n 4"
```

This can be helpful for debugging.

One other problem you might run into is that different systems use different characters to indicate the end of a line. Some systems use a newline, represented `\n`. Others use a return character, represented `\r`. Some use both. If you move files between different systems, these inconsistencies can cause problems.

For most systems, there are applications to convert from one format to another. You can find them (and read more about this issue) at [https://en.wikipedia.org/wiki/Newline](https://en.wikipedia.org/wiki/Newline). Or, of course, you could write one yourself.

#### Glossary (14)

##### persistent

Pertaining to a program that runs indefinitely and keeps at least some of its data in permanent storage.

##### text file

A sequence of characters stored in permanent storage like a hard drive.

##### directory

A named collection of files, also called a folder.

##### path

A string that identifies a file.

##### relative path

A path that starts from the current directory.

##### absolute path

A path that starts from the topmost directory in the file system.

##### catch

To prevent an exception from terminating a program using the `try ... catch ... finally` statements.

##### database

A file whose contents are organized like a dictionary with keys that correspond to values.

##### shell

A program that allows users to type commands and then executes them by starting other programs.

##### command object

An object that represents a shell command, allowing a Julia program to run commands and read the results.




### 15. Structs and objects  


#### Composite types
A programmer-defined _composite type_ is also called a _struct_. The `struct` definition for a point looks like this:

```
struct Point
    x
    y
end
```


The header indicates that the new struct is called `Point`. The body defines the _attributes_ or _fields_ of the struct. The `Point` struct has two fields: `x` and `y`.

A struct is like a factory for creating objects. To create a point, you call `Point` as if it were a function having as arguments the values of the fields. When `Point` is used as a function, it is called a _constructor_.

```
julia> p = Point(3.0, 4.0)
Point(3.0, 4.0)
```

Creating a new object is called _instantiation_, and the object is an _instance_ of the type.

When you print an instance, Julia tells you what type it belongs to and what the values of the atributes are.


#### Structs are Immutable

You can get the values of the fields using `.` notation:

```
julia> x = p.x
3.0
julia> p.y
4.0
```
The expression `p.x` means, “Go to the object `p` refers to and get the value of `x`.” In the example, we assign that value to a variable named `x`. There is no conflict between the variable `x` and the _field_ `x`.

You can use dot notation as part of any expression. For example:

```
julia> distance = sqrt(p.x^2 + p.y^2)
5.0
```


**Structs are however by default immutable**, after construction the fields can not change value:

```
julia> p.y = 1.0
ERROR: setfield! immutable struct of type Point cannot be changed
```

This may seem odd at first, but it has several advantages:

-   It can be more efficient.
    
-   It is not possible to violate the invariants provided by the type’s constructors (see [Constructors](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#constructor)).
    
-   Code using immutable objects can be easier to reason about.


#### Mutable Structs

Where required, mutable composite types can be declared with the keyword `mutable struct`. Here is the definition of a mutable point:

```
mutable struct MPoint
    x
    y
end
```

You can assign values to an instance of a mutable struct using dot notation:

```
julia> blank = MPoint(0.0, 0.0)
MPoint(0.0, 0.0)
julia> blank.x = 3.0
3.0
julia> blank.y = 4.0
4.0
```


An object that is a field of another object is _embedded_.


#### Instances as Arguments

You can pass an instance as an argument in the usual way. For example:

```
function printpoint(p)
    println("($(p.x), $(p.y))")
end
```

`printpoint` takes a `Point` as an argument and displays it in mathematical notation. To invoke it, you can pass `p` as an argument:

```
julia> printpoint(blank)
(3.0, 4.0)
```

If a mutable struct object is passed to a function as an argument, the function can modify the fields of the object. For example, `movepoint!` takes a mutable `Point` object and two numbers, `dx` and `dy`, and adds the numbers to respectively the `x` and the `y` attribute of the `Point`:

```
function movepoint!(p, dx, dy)
    p.x += dx
    p.y += dy
    nothing
end
```

Here is an example that demonstrates the effect:

```
julia> origin = MPoint(0.0, 0.0)
MPoint(0.0, 0.0)
julia> movepoint!(origin, 1.0, 2.0)

julia> origin
MPoint(1.0, 2.0)
```

Inside the function, `p` is an alias for `origin`, so when the function modifies `p`, `origin` changes.

Passing an immutable `Point` object to `movepoint!` causes an error:

```
julia> movepoint!(p, 1.0, 2.0)
ERROR: setfield! immutable struct of type Point cannot be changed
```

You can however modify the value of a mutable attribute of an immutable object.

WARNING. You cannot reassign a mutable attribute of an immutable object:
```
julia> box.corner = MPoint(1.0, 2.0)
ERROR: setfield! immutable struct of type Rectangle cannot be changed
```


#### Instances as return values
Functions can return instances. For example, `findcenter` takes a `Rectangle` as an argument and returns a `Point` that contains the coordinates of the center of the rectangle:

```
function findcenter(rect)
    Point(rect.corner.x + rect.width / 2, rect.corner.y + rect.height / 2)
end
```

The expression `rect.corner.x` means, “Go to the object `rect` refers to and select the field named `corner`; then go to that object and select the field named `x`.”


#### Copying
Aliasing can make a program difficult to read because changes in one place might have unexpected effects in another place. It is hard to keep track of all the variables that might refer to a given object.

Copying an object is often an alternative to aliasing. Julia provides a function called `deepcopy` that can duplicate any object:

```
julia> p1 = MPoint(3.0, 4.0)
MPoint(3.0, 4.0)
julia> p2 = deepcopy(p1)
MPoint(3.0, 4.0)
julia> p1 ≡ p2
false
julia> p1 == p2
false
```

The `≡` operator indicates that `p1` and `p2` are not the same object, which is what we expected. But you might have expected `==` to yield `true` because these points contain the same data. In that case, you will be disappointed to learn that for mutable objects, the default behavior of the `==` operator is the same as the `===` operator; it checks object identity, not object equivalence. That’s because for mutable composite types, Julia doesn’t know what should be considered equivalent. At least, not yet.


#### Debugging (15)
When you start working with objects, you are likely to encounter some new exceptions. If you try to access a field that doesn’t exist, you get:

```
julia> p = Point(3.0, 4.0)
Point(3.0, 4.0)
julia> p.z = 1.0
ERROR: type Point has no field z
Stacktrace:
 [1] setproperty!(::Point, ::Symbol, ::Float64) at ./sysimg.jl:19
 [2] top-level scope at none:0
```

If you are not sure what type an object is, you can ask:

```
julia> typeof(p)
Point
```

You can also use `isa` to check whether an object is an instance of a type:

```
julia> p isa Point
true
```

If you are not sure whether an object has a particular attribute, you can use the built-in function `fieldnames`:

```
julia> fieldnames(Point)
(:x, :y)
```

or the function `isdefined`:

```
julia> isdefined(p, :x)
true
julia> isdefined(p, :z)
false
```

The first argument can be any object; the second argument is a symbol, `:` followed by the name of the field.


#### Glossary (15)

##### struct

A composite type.

##### constructor

A function with the same name as a type that creates instances of the type.

##### instance

An object that belongs to a type.

##### instantiate

To create a new object.

##### attribute or field

One of the named values associated with an object.

##### embedded object

An object that is stored as a field of another object.

##### deep copy

To copy the contents of an object as well as any embedded objects, and any objects embedded in them, and so on; implemented by the `deepcopy` function.

##### object diagram

A diagram that shows objects, their fields, and the values of the fields.





### 16. Structs and Functions 
Now that we know how to create new composite types, the next step is to write functions that take programmer-defined objects as parameters and return them as results. In this chapter I also present “functional programming style” and two new program development plans.


#### Pure Functions
In the next few sections, we’ll write two functions that add time values. They demonstrate two kinds of functions: pure functions and modifiers. They also demonstrate a development plan I’ll call _prototype and patch_, which is a way of tackling a complex problem by starting with a simple prototype and incrementally dealing with the complications.

Here is a simple prototype of `addtime`:

```
function addtime(t1, t2)
    MyTime(t1.hour + t2.hour, t1.minute + t2.minute, t1.second + t2.second)
end
```

The function creates a new `MyTime` object, initializes its fields, and returns a reference to the new object. This is called a _pure function_ because it does not modify any of the objects passed to it as arguments and it has no effect, like displaying a value or getting user input, other than returning a value.

#### Modifiers
Sometimes it is useful for a function to modify the objects it gets as parameters. In that case, the changes are visible to the caller. Functions that work this way are called _modifiers_.

Anything that can be done with modifiers can also be done with pure functions. In fact, some programming languages only allow pure functions. There is some evidence that programs that use pure functions are faster to develop and less error-prone than programs that use modifiers. But modifiers are convenient at times, and functional programs tend to be less efficient.

In general, I recommend that you write pure functions whenever it is reasonable and resort to modifiers only if there is a compelling advantage. This approach might be called a _functional programming style_.

#### Prototyping versus Planning
The development plan I am demonstrating is called “prototype and patch”. For each function, I wrote a prototype that performed the basic calculation and then tested it, patching errors along the way.

This approach can be effective, especially if you don’t yet have a deep understanding of the problem. But incremental corrections can generate code that is unnecessarily complicated—since it deals with many special cases—and unreliable—since it is hard to know if you have found all the errors.

An alternative is _designed development_, in which high-level insight into the problem can make the programming much easier.

...

Ironically, sometimes making a problem harder (or more general) makes it easier (because there are fewer special cases and fewer opportunities for error).

#### Debugging (16)
A `MyTime` object is well-formed if the values of `minute` and `second` are between 0 and 60 (including 0 but not 60) and if `hour` is positive. `hour` and `minute` should be integral values, but we might allow `second` to have a fraction part.

Requirements like these are called _invariants_ because they should always be true. To put it a different way, if they are not true, something has gone wrong.

Writing code to check invariants can help detect errors and find their causes. For example, you might have a function like `isvalidtime` that takes a `MyTime` object and returns `false` if it violates an invariant:

```
function isvalidtime(time)
    if time.hour < 0 || time.minute < 0 || time.second < 0
        return false
    end
    if time.minute >= 60 || time.second >= 60
        return false
    end
    true
end
```
At the beginning of each function you could check the arguments to make sure they are valid:

```
function addtime(t1, t2)
    if !isvalidtime(t1) || !isvalidtime(t2)
        error("invalid MyTime object in add_time")
    end
    seconds = timetoint(t1) + timetoint(t2)
    inttotime(seconds)
end
```

Or you could use an `@assert` macro, which checks a given invariant and throws an exception if it fails:

```
function addtime(t1, t2)
    @assert(isvalidtime(t1) && isvalidtime(t2), "invalid MyTime object in add_time")
    seconds = timetoint(t1) + timetoint(t2)
    inttotime(seconds)
end
```

`@assert` macros are useful because they distinguish code that deals with normal conditions from code that checks for errors.

#### Glossary (16)

##### prototype and patch

A development plan that involves writing a rough draft of a program, testing, and correcting errors as they are found.

##### designed development

A development plan that involves high-level insight into the problem and more planning than incremental development or prototype development.

##### pure function

A function that does not modify any of the objects it receives as arguments. Most pure functions are fruitful.

##### modifier

A function that changes one or more of the objects it receives as arguments. Most modifiers are void; that is, they return `nothing`.

##### functional programming style

A style of program design in which the majority of functions are pure.

##### invariant

A condition that should never change during the execution of a program.


### 17. Multiple Dispatch
In Julia you have the ability to write code that can operate on different types. This is called generic programming.

In this chapter I will discuss the use of type declarations in Julia and I will introduce methods which are ways to implement different behavior for a function depending on the types of its arguments. This is called multiple dispatch.

#### Type Declarations
The `::` operator attaches _type annotations_ to expressions and variables:

```
julia> (1 + 2) :: Float64
ERROR: TypeError: in typeassert, expected Float64, got Int64
julia> (1 + 2) :: Int64
3
```

This helps to confirm that your program works the way you expect.

The `::` operator can also be appended to the left-hand side of an assignment, or as part of a declaration.

```
julia> function returnfloat()
           x::Float64 = 100
           x
       end
returnfloat (generic function with 1 method)
julia> x = returnfloat()
100.0
julia> typeof(x)
Float64
```

The variable `x` is always of type `Float64` and the value is converted to a floating point if needed.

A type annotation can also be attached to the header of a function definition:

```
function sinc(x)::Float64
    if x == 0
        return 1
    end
    sin(x)/(x)
end
```

The return value of `sinc` is always converted to type `Float64`.

The default behavior in Julia when types are omitted is to allow values to be of any type (`Any`).


### Methods
type declarations can and should be added for performance reasons to the fields in a struct definition. e.g.

```
using Printf

struct MyTime
    hour :: Int64
    minute :: Int64
    second :: Int64
end

function printtime(time)
    @printf("%02d:%02d:%02d", time.hour, time.minute, time.second)
end
```

To add a _method_ to the function `printtime` that only accepts as argument a `MyTime` object, all we have to do is append `::` followed by `MyTime` to the argument `time` in the function definition:

```
function printtime(time::MyTime)
    @printf("%02d:%02d:%02d", time.hour, time.minute, time.second)
end
```

A method is a function definition with a specific _signature_: `printtime` has one argument of type `MyTime`.

By the way, optional arguments are implemented as syntax for multiple method definitions. For example, this definition:

```
function f(a=1, b=2)
    a + 2b
end
```

translates to the following three methods:

```
f(a, b) = a + 2b
f(a) = f(a, 2)
f() = f(1, 2)
```

These expressions are valid Julia method definitions. This is a shorthand notation for defining functions/methods.


#### Constructors
A _constructor_ is a special function that is called to create an object.

The default constructor methods of `MyTime` have the following signatures:

```
MyTime(hour, minute, second)
MyTime(hour::Int64, minute::Int64, second::Int64)
```

We can also add our own _outer constructor_ methods:

```
function MyTime(time::MyTime)
    MyTime(time.hour, time.minute, time.second)
end
```

This method is called a _copy constructor_ because the new `MyTime` object is a copy of its argument.

To enforce invariants, we need _inner constructor_ methods:

```
struct MyTime
    hour :: Int64
    minute :: Int64
    second :: Int64
    function MyTime(hour::Int64=0, minute::Int64=0, second::Int64=0)
        @assert(0 ≤ minute < 60, "Minute is not between 0 and 60.")
        @assert(0 ≤ second < 60, "Second is not between 0 and 60.")
        new(hour, minute, second)
    end
end
```

An inner constructor method is always defined inside the block of a type declaration and it has access to a special function called `new` that creates objects of the newly declared type.

Warning. The default constructor is not available if any inner constructor is defined. You have to write explicitly all the inner constructors you need.

## NEED TO RE READ CUZ U DONT UNDERSTAND SH1T AND ARE AVOIDING PARTS

### Operator overloading
By defining operator methods, you can specify the behavior of operators on programmer-defined types. For example, if you define a method named `+` with two `MyTime` arguments, you can use the `+` operator on `MyTime` objects.

Adding to the behavior of an operator so that it works with programmer-defined types is called _operator overloading_.



### Multiple Dispatch
The choice of which method to execute when a function is applied is called _dispatch_. Julia allows the dispatch process to choose which of a function’s methods to call based on the number of arguments given, and on the types of all of the function’s arguments. Using all of a function’s arguments to choose which method should be invoked is known as _multiple dispatch_.


### Generic Programming
Multiple dispatch is useful when it is necessary, but (fortunately) it is not always necessary. Often you can avoid it by writing functions that work correctly for arguments with different types.

Functions that work with several types are called _polymorphic_. Polymorphism can facilitate code reuse.

In general, if all of the operations inside a function work with a given type, the function works with that type.

The best kind of polymorphism is the unintentional kind, where you discover that a function you already wrote can be applied to a type you never planned for.


### Interface and implementation
One of the goals of multiple dispatch is to make software more maintainable, which means that you can keep the program working when other parts of the system change, and modify the program to meet new requirements.

A design principle that helps achieve that goal is to keep interfaces separate from implementations. This means that the methods having an argument annotated with a type should not depend on how the fields of that type are represented.

For example, in this chapter we developed a struct that represents a time of day. Methods having an argument annotated with this type include `timetoint`, `isafter`, and `+`.

We could implement those methods in several ways. The details of the implementation depend on how we represent `MyTime`. In this chapter, the fields of a `MyTime` object are `hour`, `minute`, and `second`.

As an alternative, we could replace these fields with a single integer representing the number of seconds since midnight. This implementation would make some functions, like `isafter`, easier to write, but it makes other functions harder.

After you deploy a new type, you might discover a better implementation. If other parts of the program are using your type, it might be time-consuming and error-prone to change the interface.

But if you designed the interface carefully, you can change the implementation without changing the interface, which means that other parts of the program don’t have to change.


### Debugging (17)
Calling a function with the correct arguments can be difficult when more than one method for the function is specified. Julia allows to introspect the signatures of the methods of a function.

To know what methods are available for a given function, you can use the function `methods`:

```
julia> methods(printtime)
# 2 methods for generic function "printtime":
[1] printtime(time::MyTime) in Main at REPL[3]:2
[2] printtime(time) in Main at REPL[4]:2
```

In this example, the function `printtime` has 2 methods: one with a `MyTime` argument and one with an `Any` argument.


#### Glossary (17)

#### type annotation
The operator `::` followed by a type indicating that an expression or a variable is of that type.

#### method
A definition of a possible behavior for a function.

#### dispatch
The choice of which method to execute when a function is executed.

#### signature
The number and type of the arguments of a method allowing the dispatch to select the most specific method of a function during the function call.

#### outer constructor
Constructor defined outside the type definition to define convenience methods for creating an object.

#### inner constructor
Constructor defined inside the type definition to enforce invariants or to construct self-referential objects.

#### default constructor
Inner constructor that is available when no programmer-defined inner constructors are provided.

#### copy constructor
Outer constructor method of a type with as only argument an object of the type. It creates a new object that is a copy of the argument.

#### operator overloading
Adding to the behavior of an operator like `+` so it works with a programmer-defined type.

#### multiple dispatch
Dispatch based on all of a function’s arguments.

#### generic programming
Writing code that can work with more than one type.



### Subtyping
In the previous chapter we introduced the multiple dispatch mechanism and polymorphic methods. Not specifying the type of the arguments results in a method that can be called with arguments of any type. Specifying a subset of allowed types in the signature of a method is a logical next step.

...

The variables `suit_names` and `rank_names` are global variables. The `const` declaration means that the variable can only be assigned once. This solves the performance problem of global variables.

```
const suit_names = ["♣", "♦", "♥", "♠"]
const rank_names = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
```

...

### Unit Testing
_Unit testing_ allows you to verify the correctness of your code by comparing the results of your code to what you expect. This can be useful to be sure that your code still is correct after modifications, and it is also a way to predefine the correct behaviour of your code during development.

Simple unit testing can be performed with the `@test` macros:

```
julia> using Test

julia> @test Card(1, 4) < Card(2, 4)
Test Passed
julia> @test Card(1, 3) < Card(1, 4)
Test Passed
```

`@test` returns a `"Test Passed"` if the expression following it is `true`, a `"Test Failed"` if it is `false`, and an `"Error Result"` if it could not be evaluated.


### Abstract Types and Subtyping
...
So we need a way to group related _concrete types_. In Julia this is done by defining an _abstract type_ that serves as a parent for both `Deck` and `Hand`. This is called _subtyping_
...

### Type diagrams
So far we have seen stack diagrams, which show the state of a program, and object diagrams, which show the attributes of an object and their values. These diagrams represent a snapshot in the execution of a program, so they change as the program runs.

They are also highly detailed; for some purposes, too detailed. A _type diagram_ is a more abstract representation of the structure of a program. Instead of showing individual objects, it shows types and the relationships between them.

There are several kinds of relationship between types:

-   Objects of a concrete type might contain references to objects of another type. For example, each Rectangle contains a reference to a Point, and each Deck contains references to an array of Cards. This kind of relationship is called _HAS-A_, as in, “a Rectangle has a Point”.
    
-   A concrete type can have an abstract type as a supertype. This relationship is called _IS-A_, as in, “a Hand is a kind of a CardSet.”
    
-   One type might depend on another in the sense that objects of one type take objects of the second type as parameters, or use objects of the second type as part of a computation. This kind of relationship is called a _dependency_.


![[Pasted image 20220810113747.png]]

The arrow with a hollow triangle head represents an IS-A relationship; in this case it indicates that Hand has as supertype CardSet.

The standard arrow head represents a HAS-A relationship; in this case a Deck has references to Card objects.

The star (`*`) near the arrow head is a _multiplicity_; it indicates how many Cards a Deck has. A multiplicity can be a simple number, like `52`, a range, `like 5:7` or a star, which indicates that a Deck can have any number of Cards.

There are no dependencies in this diagram. They would normally be shown with a dashed arrow. Or if there are a lot of dependencies, they are sometimes omitted.

A more detailed diagram might show that a Deck actually contains an array of Cards, but built-in types like array and dictionnaries are usually not included in type diagrams.

### Debugging (18)
Any time you are unsure about the flow of execution through your program, the simplest solution is to add print statements at the beginning of the relevant methods. If `shuffle!` prints a message that says something like `Running shuffle! Deck`, then as the program runs it traces the flow of execution.

As better alternative, you can also use the `@which` macro:

```
julia> @which sort!(hand)
sort!(hand::Hand) in Main at REPL[5]:1
```

So the `sort!` method for `hand` is the one having as argument an object of type `Hand`.

...

### Data encapsulation
The previous chapters demonstrate a development plan we might call “type-oriented design”. We identified objects we needed—like `Point`, `Rectangle` and `MyTime`—and defined structs to represent them. In each case there is an obvious correspondence between the object and some entity in the real world (or at least a mathematical world).

But sometimes it is less obvious what objects you need and how they should interact. In that case you need a different development plan. In the same way that we discovered function interfaces by encapsulation and generalization, we can discover type interfaces by _data encapsulation_.

...

This example suggests a development plan for designing types:

-   Start by writing functions that read and write global variables (when necessary).
    
-   Once you get the program working, look for associations between global variables and the functions that use them.
    
-   Encapsulate related variables as fields of a struct.
    
-   Transform the associated functions into methods with as argument objects of the new type.


### Glossary (18)

#### encode

To represent one set of values using another set of values by constructing a mapping between them.

#### unit testing

Standardized way to test the correctness of code.

#### veneer

A method or function that provides a different interface to another function without doing much computation.

#### subtyping

The ability to define a hierarchy of related types.

#### abstract type

A type that can act as a parent for another type.

#### concrete type

A type that can be constructed.

#### subtype

A type that has as parent an abstract type.

#### supertype

An abstract type that is the parent of another type.

#### IS-A relationship

A relationship between a subtype and its supertype.

#### HAS-A relationship

A relationship between two types where instances of one type contain references to instances of the other.

#### dependency

A relationship between two types where instances of one type use instances of the other type, but do not store them as fields.

#### type diagram

A diagram that shows the types in a program and the relationships between them.

#### multiplicity

A notation in a type diagram that shows, for a HAS-A relationship, how many references there are to instances of another class.

#### data encapsulation

A program development plan that involves a prototype using global variables and a final version that makes the global variables into instance fields.


### 19. The Goodies: Syntax

This chapter and the next discuss the things I have left out in the previous chapters:

-   syntax supplements
    
-   functions, types and macros directly available in `Base`
    
-   functions, types and macros in the Standard Library.


### Named Tuples

You can name the components of a tuple, creating a named tuple:

```
julia> x = (a=1, b=1+1)
(a = 1, b = 2)
julia> x.a
1
```

With named tuples, fields can be accessed by name using dot syntax `(x.a)`.

### Functions

Function in Julia can be defined by a compact syntax.

```
julia> f(x,y) = x + y
f (generic function with 1 method)
```

#### Anonymous Functions

We can define a function without specifying a name:

```
julia> x -> x^2 + 2x - 1
#1 (generic function with 1 method)
julia> function (x)
           x^2 + 2x - 1
       end
#3 (generic function with 1 method)
```

These are example of _anonymous functions_. Anonymous functions are often used as an argument to another function:

```
julia> using Plots

julia> plot(x -> x^2 + 2x - 1, 0, 10, xlabel="x", ylabel="y")
```

#### Keyword Arguments
Function arguments can also be named:

```
julia> function myplot(x, y; style="solid", width=1, color="black")
           ###
       end
myplot (generic function with 1 method)
julia> myplot(0:10, 0:10, style="dotted", color="blue")
```

_Keyword arguments_ are named arguments in a function and are specified after a semicolon in the signature but can be called with a comma.


#### Closures

A _closure_ is a technique allowing a function to capture a variable defined outside the calling scope of the function.

```
julia> foo(x) = ()->x
foo (generic function with 1 method)

julia> bar = foo(1)
#1 (generic function with 1 method)

julia> bar()
1
```

In this example, the function `foo` returns an anonymous function that has access to the `x` argument of the function `foo`. `bar` points to the anonymous function and returns the value of the argument of `foo`.

### Blocks

A _block_ is a way to group a number of statements. A block starts with the keyword `begin` and ends with `end`.

In [Case Study: Interface Design](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#chap04) the `@svg` macro was introduced:

```
🐢 = Turtle()
@svg begin
    forward(🐢, 100)
    turn(🐢, -90)
    forward(🐢, 100)
end
```

In this example, the macro `@svg` has a single argument, i.e. a block grouping 3 function calls.


#### `let` Blocks

A `let` block is useful to create new bindings, i.e. locations that can refer to values.

```
julia> x, y, z = -1, -1, -1;

julia> let x = 1, z
           @show x y z;
       end
x = 1
y = -1
ERROR: UndefVarError: z not defined
julia> @show x y z;
x = -1
y = -1
z = -1
```

In the example, the first `@show` macro, shows the local `x`, the global `y` and the undefined local `z`. The global variables are untouched.

#### `do` Blocks

...

### Control Flow

#### Ternary Operator

The _ternary operator_, `?:`, is an alternative to an `if-elseif` statement used when you need to make a choice between single expression values.

```
julia> a = 150
150
julia> a % 2 == 0 ? println("even") : println("odd")
even
```

The expression before the `?` is a condition expression. If the condition is `true`, the expression before the `:` is evaluated, otherwise, the expression after the `:` is evaluated.


#### Short-Circuit Evaluation

The operators `&&` and `||` do a _short-circuit evaluation_: a next argument is only evaluated when it is needed to determine the final value.

For example, a recursive factorial routine could be defined like this:

```
function fact(n::Integer)
    n >= 0 || error("n must be non-negative")
    n == 0 && return 1
    n * fact(n-1)
end
```


#### Tasks (aka Coroutines)
...

### Types

#### Primitive Types

A concrete type consisting of plain old bits is called a _primitive type_. Unlike most languages, with Julia you can declare your own primitive types. The standard primitive types are defined in the same way:

```
primitive type Float64 <: AbstractFloat 64 end
primitive type Bool <: Integer 8 end
primitive type Char <: AbstractChar 32 end
primitive type Int64 <: Signed 64 end
```

The number in the statements specifies how many bits are required.

The following example creates a primitive type `Byte` and a constructor:

```
julia> primitive type Byte 8 end

julia> Byte(val::UInt8) = reinterpret(Byte, val)
Byte
julia> b = Byte(0x01)
Byte(0x01)
```

The function `reinterpret` is used to store the bits of an unsigned integer with 8 bits (`UInt8`) into the byte.


#### Parametric Types

Julia’s type system is _parametric_, meaning that types can have parameters.

Type parameters are introduced after the name of the type, surrounded by curly braces:

```
struct Point{T<:Real}
    x::T
    y::T
end
```

This defines a new parametric type, `Point{T<:Real}`, holding two "coordinates" of type `T`, which can be any type having `Real` as supertype.

```
julia> Point(0.0, 0.0)
Point{Float64}(0.0, 0.0)
```

In addition to composite types, abstract types and primitive types can also have a type parameter.

Tip

Having concrete types for struct fields is absolutely recommended for performance reasons, so this is a good way to make `Point` both fast and flexible.

#### Type Unions

...

### Methods

#### Parametric Methods

...

#### Function-like Objects
...


### Constructors

Parametric types can be explicitly or implicitly constructed:

```
julia> Point(1,2)         # implicit T
Point{Int64}(1, 2)
julia> Point{Int64}(1, 2) # explicit T
Point{Int64}(1, 2)
julia> Point(1,2.5)       # implicit T
ERROR: MethodError: no method matching Point(::Int64, ::Float64)
```

...

### Conversion and Promotion

Julia has a system for promoting arguments to a common type. This is not done automatically but can be easily extended.

#### Conversion

A value can be converted from one type to another:

```
julia> x = 12
12
julia> typeof(x)
Int64
julia> convert(UInt8, x)
0x0c
julia> typeof(ans)
UInt8
```

...

#### Promotion

_Promotion_ is the conversion of values of mixed types to a single common type:

```
julia> promote(1, 2.5, 3)
(1.0, 2.5, 3.0)
```

Methods for the `promote` function are normally not directly defined, but the auxiliary function `promote_rule` is used to specify the rules for promotion:

```
promote_rule(::Type{Float64}, ::Type{Int32}) = Float64
```


### Metaprogramming

Julia code can be represented as a data structure of the language itself. This allows a program to transform and generate its own code.

#### Expressions

Every Julia program starts as a string:

```
julia> prog = "1 + 2"
"1 + 2"
```

The next step is to parse each string into an object called an _expression_, represented by the Julia type `Expr`:

```
julia> ex = Meta.parse(prog)
:(1 + 2)
julia> typeof(ex)
Expr
julia> dump(ex)
Expr
  head: Symbol call
  args: Array{Any}((3,))
    1: Symbol +
    2: Int64 1
    3: Int64 2
```

The `dump` function displays expr objects with annotations.

Expressions can be constructed directly by prefixing with `:` inside parentheses (i guess this is :("1+2") or something like that) or using a quote block

```
julia> ex = quote
           1 + 2
       end;
```

#### `eval`

Julia can evaluate an expression object using `eval`:

```
julia> eval(ex)
3
```

Every module has its own `eval` function that evaluates expressions in its scope.

**Warning.** When you are using a lot of calls to the function `eval`, often this means that something is wrong. `eval` is considered “evil”.

#### Macros
...

#### Generated Functions
...

### Missing Values

_Missing values_ can be represented via the `missing` object, which is the singleton instance of the type `Missing`.

Arrays can contain missing values:

```
julia> a = [1, missing]
2-element Array{Union{Missing, Int64},1}:
 1
  missing
```

The element type of such an array is `Union{Missing, T}`, with `T` the type of the non-missing values.

Reduction functions return `missing` when called on arrays which contain missing values

```
julia> sum(a)
missing
```

In this situation, use the `skipmissing` function to skip missing values:

```
julia> sum(skipmissing([1, missing]))
1
```


### Glossary (19)

#### closure

Function that captures variables from its defining scope.

#### let block

Block allocating new variable bindings.

#### anonymous function

Function defined without being given a name.

#### named tuple

Tuple with named components.

#### keyword arguments

Arguments identified by name instead of only by position.

#### do block

Syntax construction used to define and call an anonymous function which looks like a normal code block.

#### ternary operator

Control flow operator taking three operands to specify a condition, an expression to be executed when the condition yields `true` and an expression to be executed when the condition yields `false`.

#### short-circuit evaluation

Evaluation of a boolean operator for which the second argument is executed or evaluated only if the first argument does not suffice to determine the value of the expression.

#### task (aka coroutine)

Control flow feature that allows computations to be suspended and resumed in a flexible manner.

#### primitive type

Concrete type whose data consists of plain old bits.

#### type union

Type which includes as objects all instances of any of its type parameters.

#### parametric type

Type that is parameterized.

#### functor

Object with an associated method, so that it is callable.

#### conversion

Conversion allows to convert a value from one type to another.

#### promotion

Converting values of mixed types to a single common type.

#### expression

Julia type that holds a language construct.

#### macro

Way to include generated code in the final body of a program.

#### generated functions

Functions capable of generating specialized code depending on the types of the arguments.

#### missing values

Instances that represent data points with no value.


### 20. The goodies: Base and Standard Library
Julia comes with batteries included. The `Base` module contains the most useful functions, types and macros. These are directly available in Julia.

Julia provides also a large number of specialized modules in its Standard Library (Dates, Distributed Computing, Linear Algebra, Profiling, Random Numbers, …​). Functions, types and macros defined in the Standard Library have to be imported before they can be used:

-   `import _Module_` imports the module, and `_Module.fn_(x)` calls the function `_fn_`
    
-   `using _Module_` imports all exported `_Module_` functions, types and macros.

### Measuring Performance
...

### Collections and Data Structures
...

### Mathematics
...

### Strings
...

### Arrays
...

### Interfaces
...

### Interactive Utilities
...




### Glosssary (20)
#### regex

Regular expression, a sequence of characters that define a search pattern.

#### matrix

Two-dimensional array.

#### intermediate representation

Data structure used internally by a compiler to represent source code.

#### machine code

Language instructions that can be executed directly by a computer’s central processing unit.

#### debug logging

Storing debug messages in a log.



### Debugging (21)

