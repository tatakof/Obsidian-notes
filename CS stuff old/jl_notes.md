### Structures (`struct`)

"Structures (previously known in Julia as "Types") are, for the most (see later for the difference), what in other languages are called classes, or "structured data": they define the kind of information that is embedded in the structure, that is a set of fields (aka "properties" in other languages), and then individual instances (or "objects") can be produced each with its own specific values for the fields defined by the structure.

They are "composite" types, in the sense that are not made of just a fixed amound of bits as instead "primitive" types.

- `a::B` means "a must be of type B"
- `A<:B` means "A must be a subtype of B".
"



### Metaprogramming
In R we dont use metaprogramming much (we only tend to use ... but for a datascience pipeline its not something we tipically use mucho). On the other hand, julia has a ton of metaprogramming that's used all the time. 



"Julia represents its own code as a data structure accessible from the language itself. Since code is represented by objects that can be created and manipulated from within the language, it is possible for a program to transform and generate its own code, that is to create powerful macros (the term "metaprogramming" refers to the possibility to write code that writes code that is then evaluated)."

