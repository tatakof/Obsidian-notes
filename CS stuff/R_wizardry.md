#### Dynamic variables 
programmatically define the name of a variable that's at the left side of the assignment operator

**objective**
```
```r
for (i in 1:10) {

 str_c("variable_", i) <- i

}
```




**Solution**
```r
for (i in 1:10) {
  assign(paste0("variable_", i), i)
}
```
or 

```r
for(i in 1:10){
     .GlobalEnv[[paste0("variable_", i)]] <- i
}
```