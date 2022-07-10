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


### Modifying a data structure
Same as with ###Iteration, in R you can modify in place (explain) vectors, and thus every data structure you use (remember everything in R is a vector). But in python this can't be done with all data structures (e.g.) and when you do it, you do it in a different way (append).




### Sources to learn...