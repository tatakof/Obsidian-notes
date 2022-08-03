### Getting help
Documentation can be accessed in the REPL or in a notebook by typing ? followed by the name of a function or macro, and pressing `ENTER`:

```
help?> polyline
search:

  polyline(t, n, len, angle)

  Draws n line segments with the given length and angle (in degrees) between them. t is a turtle.
```
Docstrings are often triple-quoted strings, also known as multiline strings because the triple quotes allow the string to span more than one line.

A docstring contains the essential information someone would need to use this function. It explains concisely what the function does (without getting into the details of how it does it). It explains what effect each parameter has on the behavior of the function and what type each parameter should be (if it is not obvious).

Tip: Writing this kind of documentation is an important part of interface design. A well-designed interface should be simple to explain; if you have a hard time explaining one of your functions, maybe the interface could be improved.




### Managing packages
first enter the pkg REPL by typing `]` in the terminal. 

you can install packages by typing 
```julia
pkg> add packageName
```

if you are in a julia project, this will add the package to the current project, and by default, does it by cloning Julia's general registry. 

You can check the status of your proyect library by running 
`]st`

```julia
pkg> st
```

you can check the status of all the packages in the environment (including recursive dependencies), by running:
```julia
pkg> st --manifest
```

you can add multiple packages in one command like so: 

```julia
pkg> add packageName1 packageName2
```

you can install a specific version of a package likeso (example with v0.8.8): 
```julia
pkg> add packageName@packageVersion

#Example
pkg> add packageName@0.8.8
```


You can add packages by running in your script or julia REPL: 

```julia
julia> using packageName
```





### Expressions

Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (we will see exceptions to this rule later).






### Functions
In the context of programming, a _function_ is a named sequence of statements that performs a computation. When you define a function, you specify the name and the sequence of statements. Later, you can “call” the function by name.

The expression in parentheses is called the _argument_ of the function

It is common to say that a function “takes” an argument and “returns” a result. The result is also called the _return value_.

In Julia, most of the familiar mathematical functions are directly available

```julia
result = 5 * log10(10)

degrees = 90
radians = degrees / 180 * \pi 
result2 = sin(radians)
```

#### Function definition

A _function definition_ specifies the name of a new function and the sequence of statements that run when the function is called. Here is an example:

```julia
function printlyrics()
    println("I'm a lumberjack, and I'm okay.")
    println("I sleep all night and I work all day.")
end
```

The rules for function names are the same as for variable names: they can contain almost all Unicode characters (see [Characters](https://benlauwens.github.io/ThinkJulia.jl/latest/book.html#characters)), but the first character can’t be a number. You can’t use a keyword as the name of a function, and you should avoid having a variable and a function with the same name.

The empty parentheses after the name indicate that this function doesn’t take any arguments.

The first line of the function definition is called the _header_; the rest is called the _body_. The body is terminated with the keyword `end` and it can contain any number of statements. For readability the body of the function should be indented.

The quotation marks must be “straight quotes”, usually located next to Enter on the keyboard. “Curly quotes”, like the ones in this sentence, are not legal in Julia.

Function definitions get executed just like other statements, but the effect is to create function objects. The statements inside the function do not run until the function is called, and the function definition generates no output.

As you might expect, you have to create a function before you can run it. In other words, the function definition has to run before the function gets called.




Void functions might display something on the screen or have some other effect, but they don’t have a return value. If you assign the result to a variable, you get a special value called `nothing`.

(in julia) To print the value `nothing`, you have to use the function `show` which is like `print` but can handle the value `nothing`.


-   In Julia, functions can improve performance a lot.




#### Flow of execution

Function definitions do not alter the flow of execution of the program, but remember that statements inside the function don’t run until the function is called.


A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, runs the statements there, and then comes back to pick up where it left off.

That sounds simple enough, until you remember that one function can call another. While in the middle of one function, the program might have to run the statements in another function. Then, while running that new function, the program might have to run yet another function!

In summary, when you read a program, you don’t always want to read from top to bottom. Sometimes it makes more sense if you follow the flow of execution.

### Incremental development of Functions

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




### Useful things julia provides
Julia provides the function `factorial` to calculate the factorial of an integer number.

EMOJIS
\:banana: TAB


### Checking Types
check if a variable is an integer
```
var = 5
var isa Int64
```

### Strings
A string is a sequence of characters. You can access the characters one at a time with the bracket operator:

```
julia> fruit = "banana"
"banana"
julia> letter = fruit[1]
'b': ASCII/Unicode U+0062 (category Ll: Letter, lowercase)
```


### Indexing
```
julia> letter = fruit[1]
```

The expression in brackets is called an _index_. The index indicates which character in the sequence you want (hence the name).

All indexing in Julia is 1-based—the first element of any integer-indexed object is found at index 1 and the last element at index `end`:

```
julia> fruit[end]
'a': ASCII/Unicode U+0061 (category Ll: Letter, lowercase)
```

As an index you can use an expression that contains variables and operators:

```
julia> i = 1
1
julia> fruit[i+1]
'a': ASCII/Unicode U+0061 (category Ll: Letter, lowercase)
julia> fruit[end-1]
'n': ASCII/Unicode U+006e (category Ll: Letter, lowercase)
```

But the value of the index has to be an integer. Otherwise you get:

```
julia> letter = fruit[1.5]
ERROR: MethodError: no method matching getindex(::String, ::Float64)
```

But the value of the index has to be an integer. Otherwise you get:

```
julia> letter = fruit[1.5]
ERROR: MethodError: no method matching getindex(::String, ::Float64)
```

`ength` is a built-in function that returns the number of characters in a string:

```
julia> fruits = "🍌 🍎 🍐"
"🍌 🍎 🍐"
julia> len = length(fruits)
5
```

To get the last letter of a string, you might be tempted to try something like this:

```
julia> last = fruits[len]
' ': ASCII/Unicode U+0020 (category Zs: Separator, space)
```

But you might not get what you expect.

Strings are encoded using the _UTF-8 encoding_. UTF-8 is a variable-width encoding, meaning that not all characters are encoded in the same number of bytes.

The function `sizeof` gives the number of bytes in a string:

```
julia> sizeof("🍌")
4
```

Because an emoji is encoded in 4 bytes and string indexing is byte based, the 5th element of `fruits` is a `SPACE`.

This means also that not every byte index into a UTF-8 string is necessarily a valid index for a character. If you index into a string at such an invalid byte index, an error is thrown:

```
julia> fruits[2]
ERROR: StringIndexError("🍌 🍎 🍐", 2)
```

In the case of `fruits`, the character `🍌` is a four-byte character, so the indices 2, 3 and 4 are invalid and the next character’s index is 5; this next valid index can be computed by `nextind(fruits, 1)`, and the next index after that by `nextind(fruits, 5)` and so on.






### Length vs sizeof






#### Strings are immutable (unlike in R)

It is tempting to use the `[]` operator on the left side of an assignment, with the intention of changing a character in a string. For example:

```
julia> greeting = "Hello, world!"
"Hello, world!"
julia> greeting[1] = 'J'
ERROR: MethodError: no method matching setindex!(::String, ::Char, ::Int64)
```

The reason for the error is that strings are _immutable_, which means you can’t change an existing string. The best you can do is create a new string that is a variation on the original:

```
julia> greeting = "J" * greeting[2:end]
"Jello, world!"
```
This example concatenates a new first letter onto a slice of greeting. It has no effect on the original string (m'because there's variable updating).


#### String interpolation
Constructing strings using concatenation can become a bit cumbersome. To reduce the need for these verbose calls to `string` or repeated multiplications, Julia allows _string interpolation_ using `$`:

```
julia> greet = "Hello"
"Hello"
julia> whom = "World"
"World"
julia> "$greet, $(whom)!"
"Hello, World!"
```
m' note that the parenthesis is used to add the !, because otherwise we would be telling julia that we want to interpolate a variable called `whom!`` 

This is more readable and convenient than string concatenation: `greet * ", " * whom * "!"`

The shortest complete expression after the `$` is taken as the expression whose value is to be interpolated into the string. Thus, you can interpolate any expression into a string using parentheses:

```
julia> "1 + 2 = $(1 + 2)"
"1 + 2 = 3"
```


Julia does not handle uppercase and lowercase letters the same way people do. All the uppercase letters come before all the lowercase letters, so:

Your word, Pineapple, comes before banana.

Tip
A common way to address this problem is to convert strings to a standard format, such as all lowercase, before performing the comparison.








### Assignment operator
At this point I want to address a common source of confusion. Because Julia uses the equal sign (`=`) for assignment, it is tempting to interpret a statement like `a = b` as a mathematical proposition of equality; that is, the claim that `a` and `b` are equal. But this interpretation is wrong.

First, equality is a symmetric relationship and assignment is not. For example, in mathematics, if a=7

then 7=a

. But in Julia, the statement `a = 7` is legal and `7 = a` is not.

Also, in mathematics, a proposition of equality is either true or false for all time. If a=b

now, then a will always equal b

. In Julia, an assignment statement can make two variables equal, but they don’t have to stay that way:

```
julia> a = 5
5
julia> b = a    # a and b are now equal
5
julia> a = 3    # a and b are no longer equal
3
julia> b
5
```
Reassigning variables is often useful, but you should use it with caution. If the values of variables change frequently, it can make the code difficult to read and debug.

It is illegal to define a function that has the same name as a previously defined variable.

#### Updating variables
A common kind of reassignment is an update, where the new value of the variable depends on the old.

```
julia> x = x + 1
8
```

If you try to update a variable that doesn’t exist, you get an error, because Julia evaluates the right side before it assigns a value to `x`:

```
julia> y = y + 1
ERROR: UndefVarError: y not defined
```

Before you can update a variable, you have to initialize it, usually with a simple assignment:

```
julia> y = 0
0
julia> y = y + 1
1
```




### Structures (`struct`)

"Structures (previously known in Julia as "Types") are, for the most (see later for the difference), what in other languages are called classes, or "structured data": they define the kind of information that is embedded in the structure, that is a set of fields (aka "properties" in other languages), and then individual instances (or "objects") can be produced each with its own specific values for the fields defined by the structure.

They are "composite" types, in the sense that are not made of just a fixed amound of bits as instead "primitive" types.

- `a::B` means "a must be of type B"
- `A<:B` means "A must be a subtype of B".
"






### Metaprogramming
In R we dont use metaprogramming much (we only tend to use ... but for a datascience pipeline its not something we tipically use mucho). On the other hand, julia has a ton of metaprogramming that's used all the time. 



"Julia represents its own code as a data structure accessible from the language itself. Since code is represented by objects that can be created and manipulated from within the language, it is possible for a program to transform and generate its own code, that is to create powerful macros (the term "metaprogramming" refers to the possibility to write code that writes code that is then evaluated)."





### Keywords 
... Julia’s _keywords_. The REPL uses keywords to recognize the structure of the program, and they cannot be used as variable names.

Julia has these keywords:

abstract type    baremodule   begin      break       catch
const            continue     do         else        elseif
end              export       finally    for         function
global           if           import     importall   in
let              local        macro      module      mutable struct
primitive type   quote        return     try         using
struct           where        while


You don’t have to memorize this list. In most development environments, keywords are displayed in a different color; if you try to use one as a variable name, you’ll know.







### Operator precedence

When an expression contains more than one operator, the order of evaluation depends on the _operator precedence_. For mathematical operators, Julia follows mathematical convention. The acronym _PEMDAS_ is a useful way to remember the rules:

-   _P_arentheses have the highest precedence and can be used to force an expression to evaluate in the order you want. Since expressions in parentheses are evaluated first, `2*(3-1)` is 4, and `(1+1)^(5-2)` is 8. You can also use parentheses to make an expression easier to read, as in `(minute * 100) / 60`, even if it doesn’t change the result.
    
-   _E_xponentiation has the next highest precedence, so `1+2^3` is 9, not 27, and `2*3^2` is 18, not 36.
    
-   _M_ultiplication and _D_ivision have higher precedence than _A_ddition and _S_ubtraction. So `2*3-1` is 5, not 4, and `6+4/2` is 8, not 5.
    
-   Operators with the same precedence are evaluated from left to right (except exponentiation). So in the expression `degrees / 2 * π`, the division happens first and the result is multiplied by `π`. To divide by 2π
    

, you can use parentheses, write `degrees / 2 / π` or `degrees / 2π`.






### String operations 
The `*` operator performs _string concatenation_, which means it joins the strings by linking them end-to-end.
```julia 
julia> first_str = "throat"
"throat"
julia> second_str = "warbler"
"warbler"
julia> first_str * second_str
"throatwarbler"
```

The `^` operator also works on strings; it performs repetition. For example, `"Spam"^3` is `"SpamSpamSpam"`. If one of the values is a string, the other has to be an integer.

This use of `*` and `^` makes sense by analogy with multiplication and exponentiation. Just as `4^3` is equivalent to `4*4*4`, we expect `"Spam"^3` to be the same as `"Spam"*"Spam"*"Spam"`, and it is.







### Dot notation
You can get the values of the fields using `.` notation:

```
julia> x = p.x
3.0
julia> p.y
4.0
```

The expression `p.x` means, “Go to the object `p` refers to and get the value of `x`.” In the example, we assign that value to a variable named `x`. There is no conflict between the variable `x` and the field `x`.

You can use dot notation as part of any expression. For example:









### Structs
by default immutable, but can be mutable if declared

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




### If statements
Logical operators often provide a way to simplify nested conditional statements. For example, we can rewrite the following code using a single conditional:

```
if 0 < x
    if x < 10
        println("x is a positive single-digit number.")
    end
end
```

The `print` statement runs only if we make it past both conditionals, so we can get the same effect with the `&&` operator:

```
if 0 < x && x < 10
    println("x is a positive single-digit number.")
end
```

For this kind of condition, Julia provides a more concise syntax:

```
if 0 < x < 10
    println("x is a positive single-digit number.")
end
```




### Iteration


#### For loops
The syntax of a `for` statement is similar to a function definition. It has a header and a body that ends with the keyword `end`. The body can contain any number of statements.








### Keyboard input
The programs we have written so far accept no input from the user. They just do the same thing every time.

Julia provides a built-in function called `readline` that stops the program and waits for the user to type something. When the user presses `RETURN` or `ENTER`, the program resumes and `readline` returns what the user typed as a string.

```
julia> text = readline()
What are you waiting for? ## written in repl
"What are you waiting for?"
```



### The semicolon use
A semi-colon `;` allows to put multiple statements on the same line. In the REPL only the last statement returns its value.

e.g. 
```
julia> print("What...is your name? "); readline()
What...is your name? Arthur, King of the Britons!
"Arthur, King of the Britons!"
```


#### The `!` use
As a style convention in Julia, `!` is appended to names of functions that modify their arguments.
