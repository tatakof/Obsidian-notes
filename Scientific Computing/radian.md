How to set up radian. 

I'm assuming you have the amazing R extension for VSCode by Yuki Ueda 

if not, got to the extensions panel (control shift X) and install it


![[Pasted image 20220324175412.png]]

First install radian (python package). 
github link

https://github.com/randy3k/radian


`conda install -c conda-forge radian`




The next thing we have to do is figure out what the exact path is to radian so that vscode knows how to call it, for that we have to know where radian lives in your computer. 

in linux or mac you can type in the terminal:
`which radian `

and then copy it

/home/franfram/anaconda3/bin/radian

now you go to the extensions of R

![[Screenshot from 2022-03-24 17-24-09.png]]


Open extension settings 

type rterm in the top search bar

![[Screenshot from 2022-03-24 17-33-18.png]]

R> Rterm: Linux (or Rterm Mac if you are on Mac)

and paste the path you found with `which radian`

Rterm is the name for any augmented R console that you are working with. 

The other tweak we have to do is delete the two Rterm options (--no-save and --no-restore) because they are not compatible with radian.(and that becomes a problem)
![[Screenshot from 2022-03-24 17-28-55.png]]


finally we have to go to the top search bar and write "bracketed paste", and then turn on that option ( R: Bracketed Paste)![[Screenshot from 2022-03-24 17-32-16.png]]. This has to do with how commands are sent to radian when we are trying to work with it. 




Now we are almost there but there's a good chance that if you were to try to run an R script now (remember to kill the r session first if you had one )
![[Screenshot from 2022-03-24 17-34-09.png]]

, you are gonna get a weird error where something pops up and says something beggining with "The terminal..."

The problem is that we need to give vscode just a little bit more information about where our R is installed. The way we are gonna do that is by oppening the command pallet (control shift p) and click on Open Settings (JSON) 

![[Screenshot from 2022-03-24 17-37-12.png]]

and we are gonna add a new entry into our settings. 

"terminal.integrated.env.linux": {
	"R_HOME": ""
}



and what we are doing is saying that when it opens a new terminal make sure that terminal knows about a variable called R_HOME and that R_HOME is suppoused to point to the top level of the R installation we have on our system. 

To get the path of said top level R installation, open R in the terminal
`R`
and run 
`R.home()`
copy the path (in my case `"/usr/lib/R"`)
and put it in the R_HOME above, as such 

"terminal.integrated.env.linux": {
	"R_HOME": "/usr/lib/R"
}

and your settings.json will end up looking something like this

![[Pasted image 20220324174601.png]]
and save settings.json (control s)

Now kill the R terminal again 


![[Screenshot from 2022-03-24 17-34-09.png]]


and now if you run R code it should work. 



If you like my vscode look. you can install the Glasslt-VSC extension to make your VSCode transparent (only for linux and windows) 
![[Pasted image 20220324175512.png]]




and here's the wallpaper I'm using. 

![[chill-wave.png]]


and the vscode syntax theme is Panda.

![[Pasted image 20220324175529.png]]



Problem that appears now when loading packages: 

Error: package or namespace load failed for ‘tidyverse’ in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/home/franfram/AAR-DL/renv/library/R-4.1/x86_64-pc-linux-gnu/dplyr/libs/dplyr.so':
  /home/franfram/anaconda3/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /home/franfram/AAR-DL/renv/library/R-4.1/x86_64-pc-linux-gnu/dplyr/libs/dplyr.so)


thread with many ways of solving that:
https://askubuntu.com/questions/575505/glibcxx-3-4-20-not-found-how-to-fix-this-error/764572#764572

https://stackoverflow.com/questions/65349875/where-can-i-find-glibcxx-3-4-29


Things done: 
1- 
run: 
sudo apt-get install libstdc++6 (already latest version)
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade

will check if this works (it did not). Altough, works for many packages but not for dplyr

otherwise add:
sudo apt-get dist-upgrade (didnt work)



now trying
`conda install libgcc`  # didn't work 


This finally made the trick (https://askubuntu.com/questions/575505/glibcxx-3-4-20-not-found-how-to-fix-this-error/764572#764572)

I had this issue - it was because `Anaconda2` didn't have the GLIBCXX_3.4.20 version of whatever that thing is. Only up to .19, the same as yours.

**However, Ubuntu's library did have it**. So I just created a softlink/shortcut in the Anaconda library to the actual Linux library containing that GLIBCXX_3.4.20, replacing the previous one, and it worked fine after restarting the python GUI (Spyder).

There should be a folder called `libstdc++.so.6` in the Anaconda library, which is here: `~/anaconda2/lib`. Within this folder is the versions of the script/library-code-thing, excluding the one that you're missing: GLIBCXX_3.4.20

Follow these steps to solve the issue:

1.  go to the right location and _backup_ your current `anaconda2` shortcut (change its name so it isn't overwritten): m' replace anaconda2 for whatever `which conda` outputs. 
    
    ```
    cd ~/anaconda2/lib
    mv -vf libstdc++.so.6 libstdc++.so.6.old
    ```
    
2.  create a new shortcut using the `ln` command (I am assuming that I am in the previous location ~/anaconda2/lib):
    
    ```
    ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ./libstdc++.so.6
    ```
    
3.  restart spyder / other interface you use
    

It should now work!

