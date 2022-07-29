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





### Expression
An expression is a syntactic entity in a programming language that *may be evaluated* to determine its value. It's a combination of one or more constants, variables, functions, and operators that the programming language interprets (according to its particular rules of precedence and of association) and computes to produce ("to return", in a stateful environment) another value. 
In simple settings, the resulting value is usually one of various primitive types, such as numerical, string, boolean, complex data type or other types. 

Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (we will see exceptions to this rule later).

### Syntax
The syntax of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. Applies to programming languages, source code and markup languages. 


### Primitive data types
Primitive data types are a set of basic data types from which all other data types are constructed. Specifically it often refers to the limited set of data representations in use by a particular processor, which all compiled programs must use. 

### Infix operator
A function of two arguments, with the name of the function written between the arguments. e.g. `+` (yes, that's a function, an anonymous function??) 


### Scheduler
A program that arranges jobs or a computer's operations into an appropriate sequence. 
Schedulling is the action of assigning resources to perform tasks. The resources may be processors, or other things. The tasks may be threads, processes or data flows. The scheduler is the process that carries out the activity of scheduling.  


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



Variables and parameters are local
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



#### Why Functions
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

----------------------------------------------------
Concepts from Think Julia https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#chap19

FALTA DE 3 A 14!

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





15 EN ADELANTE !!!!!!!!
### Struct 

A programmer-defined _composite type_ is also called a _struct_. The `struct` definition for a point looks like this:

```
struct Point
    x
    y
end
```


The header indicates that the new struct is called `Point`. The body defines the _attributes_ or _fields_ of the struct. The `Point` struct has two fields: `x` and `y`.

A struct is like a factory for creating objects. To create a point, you call `Point` as if it were a function having as arguments the values of the fields. When `Point` is used as a function, it is called a _constructor_.

You can get the values of the fields using `.` notation:

```
julia> x = p.x
3.0
julia> p.y
4.0
```
The expression `p.x` means, “Go to the object `p` refers to and get the value of `x`.” In the example, we assign that value to a variable named `x`. There is no conflict between the variable `x` and the field `x`.


**Structs are however by default immutable**, after construction the fields can not change value:

```
julia> p.y = 1.0
ERROR: setfield! immutable struct of type Point cannot be changed
```
This may seem odd at first, but it has several advantages:

-   It can be more efficient.
    
-   It is not possible to violate the invariants provided by the type’s constructors (see [Constructors](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#constructor)).
    
-   Code using immutable objects can be easier to reason about.

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

ESTE CAP ESTA TERMINADO? BUSCAR LO ULTIMO ESCRITO EN THINK JULIA



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




# CONTINUE AT

#### Stack Diagrams for recursive functions