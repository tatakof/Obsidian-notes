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


