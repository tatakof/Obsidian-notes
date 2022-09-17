
### Julia: How to fix slow package loading

Maybe you are trying out Julia and you find out that packages take a lot of time to load in VS Code (sometimes more than 20 seconds), which is very frustrating. Here we'll see how to fix that in less than 5 minutes. 


Open VS Code and open an empty folder previously created. 
(CTRL+Shift+p -> "open folder")

![[Pasted image 20220916180233.png]]

Create a julia environment for that julia environment so that you can control what packages you are using. 

First open a julia REPL

(CTRL+Shift+p -> "julia start repl" )

![[Pasted image 20220916180206.png]]

The julia REPL (or terminal) will be shown at the bottom by default. 

Type `]` to go to the package manager in the terminal, and type `activate .`

![[Pasted image 20220916180522.png]]

Now add all the packages that you are going to use in your project, `add package1 package2 package3`

![[Pasted image 20220916180654.png]]

Now the environment with the packages is created. 

Then click on "Julia env: vX.x" (e.g., Julia env: v1.8) at the bottom left

![[Pasted image 20220916181112.png]]

and select the julia environment (named like your folder name) as the active environment for the current window. That menas that all the code completion, inline help, will work off of this particular set of packages. 

![[Pasted image 20220916181320.png]]

Now when you load your packages in a .jl file for example, the packages loading time will be very small, instead of the 20 seconds or more you might be getting.



If you like my vscode look. you can install the Glasslt-VSC extension to make your VSCode translucent (only for linux and windows)

![[Pasted image 20220916183027.png]]

here’s the wallpaper I’m using.
![[pexels-lisa-fotios-1438248.jpg]]


and the vscode syntax theme is Github Dark Mode
![[Pasted image 20220916183140.png]]

You can also follow me on twitter (francis_felici) and github (franfram)

Cheers!