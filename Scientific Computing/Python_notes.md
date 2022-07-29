Notes on python coming from R. 

Methods are like functions in specific environments. (check)

conda is a package manager that allows the managing of both python and non-python libraries (unlike pip who only allows python libraries). 

Conda is better than pip. Always use conda for installing packages.


Don't do installations system wide (prone to screw your system). Like use renv in R, use conda environments

```
# create an environment in /envs/ 
conda create --name envname

# create environment with specific version of Python (e.g., 3.6):
conda create -n envname python=3.6


# activate an environment
conda activate envname


# install package from anaconda in current environment
conda install packagename
# or specify the environment
conda install --name envname packagename

#install multiple packages in current environment
conda install package1 package2 package3
```

If a package is not available with `conda install`, try to use another channel (locations where packages are stored, default is anaconda) like Conda-forge, which is a community channel. 

```
conda install <packagename> --channel conda-forge
```
or the bioconda channel
```
conda install <packagename? --channel bioconda

```
or simply add the conda-forge channel to your python channels
```
conda config --add channels conda-forge
```


It seems they tend to use many versions of python at the same time, both system wide and project (environment) wide. And they call each of these python installations a 'kernel'. When you run a python script or jupyter notebook, you have to choose which kernel you use. That is, if you have many system wide installations of Python, choose which version you use. And if you have many environments with specific Python and libraries installation, choose which environment to use. 







# Primer on Python for R users. (or "Coming to python from R")
from https://rstudio.github.io/reticulate/articles/python_primer.html

Python accepts tabs or spaces as the indentation spacer, but the rules get tricky when they-re mixed. Most style guides suggest (and IDE's default to) using spaces only. 


- Packing and Unpacking: 
	Tuples are the container that powers the packing and unpacking semantics in Python. Python provides the convenience of allowing you to assign multiple symbols in one expression. this is called unpacking. 
	e.g.

```
x = (1, 2, 3)
a, b, c = x
a
b
c	
```

Tuple unpacking can occur in a variety of contexts, such as iteration



- Dictionaries
	Dictionaries are most similar to R environments. They are a container where you can retrieve items by name, though in python the name (called a key in pythons parlance) does not need to be a string like in R. It can be any python object with a has() method (meaning, almost any python object). They can be created using syntax like `{key: value}`. Like Python lists, they are modified in place. Note that `r_to_py()` converts R named lists to dictionaries. 
	Like R envinroments (and unlike R's named lists), you cannot index into a dictionary with an integet to get an item at a specific index position. Dictionaries are unordered containers. (however with python 3.7 and on, dictionaries do preserve the item insertion order). 


- Sets
	Sets are a container that can be used to efficiently track unique items or deduplicate lists. They are constructed using `{val1, val2}` (like a dictionary, but without the : ). Think of them as dictionary where you only use the keys. Sets have many efficient methods for membership operations... 





### Packages
what we call packages in R is called modules in Python. 
see [[Python_notes#Python modules]]

### Getting help
if you want to get help on a method, type ?? before the method, without the module beforehand.  You can also type Module.Method?? or ??Module.Method
MAYBE MODULE IS NOT PACKAGE

doc(function_name)


### Python Kernel
In R you generally use the same version (the one downloaded) and you don't give it much thought. In Python you have to choose the kernel. 
define kernel
define python kernel
conda environment vs kernel?



### Python debugger
Using jupyter notebooks, when getting an error, type %debug in the next cell and execute it to open the Python debugger. This will allow you to inspect the content of every variable. 



## Meaning of the dot in Python
In R, the dot is just a character. In python it us used for function composition (just like R's pipe |> and magritrr's pipe %>%), ¿and it's also used to access modules from a package??

- [ ] ffffd




## OOP

Python is an object oriented programming language. **Almost everything in Python is an object, with its properties and methods**. A Class is like an object constructor, or a "blueprint" for creating objects.




### Iteration
In R, everything is a vector (yes, even matrices, tibbles and lists, which are vectors with special properties), and vectors in R are iterable objects, which means we can for example run for loops with them. And this is something we don't even think about in R, since using only one data structure (the vector), we take for granted many of the properties they have (like being iterable). But in python you have many data structures (tuples, arrays, dicts, etc) and not all of them are iterable. 
So when you start coding in python, you may try to use a for loop with one data structure and find out that you can't do it due to an error raising. Even more, in python you construct objects (or classes from which you instance an object) CHECK IF THIS RIGHT, that you have to explicitly give them the property of being iterable. 
Here are the primitive data structures (that is, those built-in python) that can be iterable: 



#### For loops
"""
For loops iterate over lists
prints:
    dog is a mammal
    cat is a mammal
    mouse is a mammal
"""
for animal in ["dog", "cat", "mouse"]:
    # You can use format() to interpolate formatted strings
    print("{} is a mammal".format(animal))

"""
"range(number)" returns an iterable of numbers
from zero to the given number
prints:
    0
    1
    2
    3
"""
for i in range(4):
    print(i)

"""
"range(lower, upper)" returns an iterable of numbers
from the lower number to the upper number
prints:
    4
    5
    6
    7
"""
for i in range(4, 8):
    print(i)

"""
"range(lower, upper, step)" returns an iterable of numbers
from the lower number to the upper number, while incrementing
by step. If step is not indicated, the default value is 1.
prints:
    4
    6
"""
for i in range(4, 8, 2):
    print(i)

"""
To loop over a list, and retrieve both the index and the value of each item in the list
prints:
    0 dog
    1 cat
    2 mouse
"""
animals = ["dog", "cat", "mouse"]
for i, value in enumerate(animals):
    print(i, value)




Python offers a fundamental abstraction called the Iterable.
An iterable is an object that can be treated as a sequence.
The object returned by the range function, is an iterable.

filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
print(our_iterable)  # => dict_keys(['one', 'two', 'three']). This is an object that implements our Iterable interface.

We can loop over it.
for i in our_iterable:
    print(i)  # Prints one, two, three

However we cannot address elements by index.
our_iterable[1]  # Raises a TypeError

An iterable is an object that knows how to create an iterator.
our_iterator = iter(our_iterable)




### Modifying a data structure
Same as with ###Iteration, in R you can modify in place (explain) vectors, and thus every data structure you use (remember everything in R is a vector). But in python this can't be done with all data structures (e.g.) and when you do it, you do it in a different way (append).




### Sources to learn...




### Python Broadcasting
see chapter 4 of fastbook and look for more sources. 

Scientific/numerical Python packages like NumPy and PyTorch will often implement broadcasting that often makes code easier to write. In the case of PyTorch, tensors with smaller rank are expanded to have the same size as the larger rank tensor. In this way, operations can be performed between tensors with different rank.


#### Python broadcasting vs R vector recycling


### Python modules
"Since modules are classes, we have to instantiate them, which is why you see `nn.ReLU()` in this example."





### List comprehension
FROM LEARN XYZ
We can use list comprehensions for nice maps and filters
List comprehension stores the output as a list which can itself be a nested list
```python 
[add_10(i) for i in [1, 2, 3]]         # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]  # => [6, 7]
```

 You can construct set and dict comprehensions as well.

```python
{x for x in 'abcddeef' if x not in 'abc'}  # => {'d', 'e', 'f'}
{x: x**2 for x in range(5)}  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```



### Unpacking
https://www.delftstack.com/howto/python/python-for-loop-multiple-variables/
A `for` loop is used for iterating over any sequence, from a list to a tuple to a dictionary. It can even iterate over a string. This article discusses how to use the `for` loop for multiple variables in Python.

The use of multiple variables in a `for` loop in Python can be applied to lists or dictionaries, but it does not work for a general error. These multiple assignments of variables simultaneously, in the same line of code, are known as **iterable unpacking**.


### Kwargs
FROM FASTAI
In Python `**kwargs` in a parameter list means "put any additional keyword arguments into a dict called `kwargs`. And `**kwargs` in an argument list means "insert all key/value pairs in the `kwargs` dict as named arguments here". This approach is used in many popular libraries, such as `matplotlib`, in which the main `plot` function simply has the signature `plot(*args, **kwargs)`. The [`plot` documentation](https://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot) says "The `kwargs` are `Line2D` properties" and then lists those properties.

  

We're using `**kwargs` in `EmbeddingNN` to avoid having to write all the arguments to `TabularModel` a second time, and keep them in sync. However, this makes our API quite difficult to work with, because now Jupyter Notebook doesn't know what parameters are available. Consequently things like tab completion of parameter names and pop-up lists of signatures won't work.