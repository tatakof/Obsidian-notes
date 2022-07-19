### Intro
https://www.juliabloggers.com/getting-started-with-julia-lang/


### Installing Julia
https://julialang.org/downloads/#current_stable_release


### Using Julia
From terminal, run `julia`
or use IDE

### REPL
The interactive session (also known as read eval print loop REPL) can be accessed by running `julia` on the terminal. 

The Julia REPL (that is, ... what in Rstudio you know as the 'console' or when you run R from the terminal) is pretty different to R. It has many different 'modes' and comes bundled with a package manager. 
When using the REPL you can press the following symbols to get into a different mode. 
- Package mode: `]`. Add and update packages, manage projects. 
- Help Mode: `?`. Search for description and examples for the built-ins (also for added packages?)
- Shell mode: `;`. Use bash shell without leaving the Julia interpreter.  


Once you are done with a given mode, pressing ESC will return to normal mode



### Installing packages
In the Julia REPL, press `]` and then type `add <packageName>` (without the usual ".jl"). E.g., `add Agents`



### Editors 
Julia is available in for many editors, such as emacs, vim, sublime text and others


### IDEs
VScode is the one with the biggest support
use julia-vscode plugin https://www.julia-vscode.org/


#### Notebooks
In R we use Rmarkdown, in Julia you can use Jupyter notebooks (which is what is normally used for python code, but can be used for R as well) https://jupyter.org/  , or Pluto notebooks, which are the new notebooks for julia that have a DAG and allow for ...   PLUTO NOTEBOOKS WEBSITE. 


Usage
##### Jupyter notebooks
First you'll need to install the IJulia package https://github.com/JuliaLang/IJulia.jl/network/members. To do so, go to the julia REPL, type `]` and then type `add IJulia` 
Just change the `interpreter` to julia?? cell language as well?

#### Pluto notebooks
First install the Pluto.jl package https://github.com/fonsp/Pluto.jl, `] add Pluto`



### Latex 
In the editor or in the Julia REPL you can use latex by writing the latex shortcut and then pressing TAB, e.g., \sqrt<TAB>, and julia will display the symbol. And also some symbols, like $\sqrt$ is also aliased to the `sqrt` function.  



### Performance tips 

"Because Julia's compiler is different from the interpreters used for languages like Python or R, you may find that Julia's performance is unintuitive at first. If you find that something is slow, we highly recommend reading through the Performance Tips section before trying anything else. Once you understand how Julia works, it's easy to write code that's nearly as fast as C."

https://docs.julialang.org/en/v1/manual/performance-tips/#man-performance-tips





### Diferences with R or Python 
https://docs.julialang.org/en/v1/manual/noteworthy-differences/#Noteworthy-differences-from-R

- To enclose strings, you must use double quotes "" instead of single quotes (in R you can enclose strings with both), single quotes in Julia only enclose characters (but i dunno whay this means)


-   left arrow is not an assignment operator

- right arrow creates an anonymous function. 

- 