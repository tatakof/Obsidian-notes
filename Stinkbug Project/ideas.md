to do: 
- state space dag
- functions to make posterior parameter plots. 



to fix: 
- fn jump sometimes redirects to main.Rmd, maybe remove it for the showdown? and check if that works (i.e., check that all functions take u to the correct file)
- ECMWF py script. Turn to jupyter notebook 
- translate plot variables and description. (post check, )
- Remove errorLens for the pitch sale
- This ignores the extra chains when there are more than 3 chains. 
```
postdata_mod1 <- bind_rows(as_tibble(samples_mod1[[1]]),

as_tibble(samples_mod1[[2]]),

as_tibble(samples_mod1[[3]]))


```

future models and stuff:
- Temp threshold
- anual climate trends. 
- add nymph data 
- add nymph population dynamics state space sub model. 


things to show: 
- shiny app
- python code to ECMWF
- maybe modify a plotting function (maybe just a lable of the posterior check function) and then show the shiny app running the pipeline with the cached targets. 
- renv lockfile and log with a function. 