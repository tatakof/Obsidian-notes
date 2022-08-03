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



# CONTINUE AT 10 ARRAYS, OBJECTS AND VALUE


# 15 EN ADELANTE !!!!!!!!
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


