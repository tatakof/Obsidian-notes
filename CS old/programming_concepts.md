### Callback: 
In computer programming, a callback, also known as a "call-after" function, is **any reference to executable code that is passed as an argument to other code; that other code is expected to call back (execute) the code at a given time**.


### Expression
An expression is a syntactic entity in a programming language that *may be evaluated* to determine its value. It's a combination of one or more constants, variables, functions, and operators that the programming language interprets (according to its particular rules of precedence and of association) and computes to produce ("to return", in a stateful environment) another value. 
In simple settings, the resulting value is usually one of various primitive types, such as numerical, string, boolean, complex data type or other types. 


### Syntax
The syntax of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. Applies to programming languages, source code and markup languages. 


### Primitive data types
Primitive data types are a set of basic data types from which all other data types are constructed. Specifically it often refers to the limited set of data representations in use by a particular processor, which all compiled programs must use. 

### Infix operator
A function of two arguments, with the name of the function written between the arguments. e.g. `+` (yes, that's a function, an anonymous function??) 


### Scheduler
A program that arranges jobs or a computer's operations into an appropriate sequence. 
Schedulling is the action of assigning resources to perform tasks. The resources may be processors, or other things. The tasks may be threads, processes or data flows. The scheduler is the process that carries out the activity of scheduling.  


### Function Signature
A function signature (or type signature, or method signature) **defines input and output of functions or methods**. A signature can include: parameters and their types. a return value and type. exceptions that might be thrown or passed back


### Casting
Casting is a way to convert values from one type to another. Mainly, two types of casting exist, Implicit casting and Explicit casting. Boxing occurs when a value type is cast to an object, or reference type. 

equivalent to type conversion?



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




### Flow of execution 
To ensure that a function is defined before its first use, you have to know the order statements run in, which is called the _flow of execution_.

Execution always begins at the first statement of the program. Statements are run one at a time, in order from top to bottom.

Function definitions do not alter the flow of execution of the program, but remember that statements inside the function don’t run until the function is called.

A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, runs the statements there, and then comes back to pick up where it left off.




CONCEPTS DE 3 A 14. 




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


