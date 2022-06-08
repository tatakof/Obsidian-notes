#### Dynamic variables 
programmatically define the name of a variable that's at the left side of the assignment operator

**Objective**
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




#### Programmatically create a named vector
```
  level_key <- character_vector_for_values %>% # these are part of the values 
    map(~{
      setNames( #setNames(VALUES, NAMES)
	    # Values
        localities,
		# Finish setting the names
        paste0(
          .x,
          '.EqNv.dat[', 
          1:n_localities, 
          ']'
        )
      )
    })

```