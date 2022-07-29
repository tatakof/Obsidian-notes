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



#### Recode a column using a predefined named vector 
```

mutate(

	new_column_name = recode(

		old_column_name, !!!named_vector[[.y]] 
		## should work without the [[.y]] but that was because my `named_vector` was a list of named vectors and I was using a map2 

)
```




#### iteratively bind cols of tibbles in a list with purrr::reduce()

![[Pasted image 20220608112959.png]] image from hadleys Advanced R
```
  # Merge all data sets inside `ridgeplot_data` list
  testt <- reduce(ridgeplot_data, bind_cols) %>% 
    # Remove duplicated columns due to bind_cols() 
    select('locality...1', starts_with(ridgeplot_params_locality)) %>% 
    # Rename locality...1
    rename('locality' = 'locality...1')

```



### Programmatically make a ggplot where one of the axis to be plotted comes from a vector (and thus is a character)
problem is that aes() wont take strings, but aes_string() can (in that case, everything u pass to aes_string must be a string, u cant pass both strings and normal variables)

```
# in this case, the variables to be programmatically plotted as X axis are in a list of tibbles in a wide format, which I THINK is needed for a ridgeplot. 
ridgeplot_global <-

map(

.x = names(params_to_plot_global),

.f = ~{

ggplot(

data = ridgeplot_data_merged,

aes_string(

x = str_c(.x, '_post_samples'),

y = 'global', fill = '..x..'

)

) +

geom_density_ridges_gradient(scale = 3, rel_min_height = 0.01) +

scale_fill_viridis(name = "Post", option = "B") +

#coord_cartesian(xlim = c(-0.5, 0.5)) +

labs(

title = str_c(.x, " parameter per global"),

x = "Posterior value"

) +

theme_bw(base_size = bs) +

theme(

legend.position = "none",

axis.title.y = element_blank(),

axis.text.y = element_text(angle = 45, size = 12),

axis.text.x = element_text(size = 12),

plot.title = element_text(size = 13)

)

}

)


```




### Advanced R filtering techniques
https://suzan.rbind.io/2018/02/dplyr-tutorial-3/


#### remove rows from a char column based on a pattern
```
# Remove all rows containing 'loglik'
data %>% filter(!str_detect(data$variable, pattern = 'loglik'))

```
#### based on many patterns

```
remove <- c("value1", "value2")

data %>% filter(!str_detect(variable, paste(remove, collapse = '|')))



```


#### Metaprogramming
##### bang bang bang (!!!)
https://www.reddit.com/r/Rlanguage/comments/g5m5bh/what_does_the_bang_bang_bang_do/ibdec5d/?context=3
[GoodAboutHood](https://www.reddit.com/user/GoodAboutHood/)

· [hace 2 a](https://www.reddit.com/r/Rlanguage/comments/g5m5bh/comment/fo4arl9/?utm_source=reddit&utm_medium=web2x&context=3) · editado hace 2 a

Let's say we want to select the first 3 columns of a data frame. So you can do something like this:

```
test_df <- tibble(a = 1, b = 1, c = 1, d = 1)

test_df %>%
  select(1, 2, 3)
```

Easy enough. Now let's say we have a list of values that we want to use to replicate the code above.

```
our_list <- list(1, 2, 3)
```

Now if you pass this to the select function it fails:

```
test_df %>%
  select(our_list)
```

That's because that code essentially translates to this:

```
test_df %>%
  select(list(1, 2, 3))
```

Which doesn't work.

What we need to do is "unpack" the list using `!!!`.

```
# This code
test_df %>%
  select(!!!our_list)

# Translates to this
test_df %>%
  select(1, 2, 3)
```

Hope this helps! Let me know if you have any questions


###### (!!!) vs unlist
Yep - `unlist()` in this case converts our list of numbers to a numerical vector. That's generally what the function does - converts a list of values to a vector of values.

```
our_list <- list(1, 2, 3)

# So this
unlist(our_list)

# Is equivalent to this
c(1, 2, 3)
```

In the case of `select()` you can select columns using a numerical vector but not a numerical list. These two are equivalent (and both work):

```
df %>%
  select(unlist(our_list))

df %>%
  select(c(1, 2, 3))
```

So let's make an example where we need `!!!`. Let's say we wanted to take a list and use it within `mutate()`.

```
library(tidyverse)

df <- tibble(a = c(1, 1, 1),
             b = c(2, 2, 2),
             c = c(3, 3, 3))

our_list <- list(d = 4, e = 5)

# This is our goal
df %>%
  mutate(d = 4,
         e = 5)
#> # A tibble: 3 × 5
#>       a     b     c     d     e
#>   <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1     1     2     3     4     5
#> 2     1     2     3     4     5
#> 3     1     2     3     4     5

# This works because we "unpack" the list
df %>%
  mutate(!!!our_list)
#> # A tibble: 3 × 5
#>       a     b     c     d     e
#>   <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1     1     2     3     4     5
#> 2     1     2     3     4     5
#> 3     1     2     3     4     5

# This doesn't work because we are converting
#   the list to numeric vector.
df %>%
  mutate(unlist(our_list))
#> Error in `mutate()`:
#> ! Problem while computing `..1 = unlist(our_list)`.
#> ✖ `..1` must be size 3 or 1, not 2.
```

If you have any questions let me know!



### How to check existence of an input argument for R functions | How to modify a function behaviour depending on the argument being passed

(https://stackoverflow.com/questions/9877271/how-to-check-existence-of-an-input-argument-for-r-functions)
HAVEN'T CHECKED THIS ONE

But an easy way is to use the `exist` function. 

You have to define a function, and inside the function body assign the argument to an object of the same name. 

```r 
function(x = example){

if (exists(example)) { #this will evaluate to true if that argument is passed 
	do_something()
	
} else {
	do_something_else()
}

}


```



### How to select columns that may or may not exist. 
Use `any_of` of the `tidyselect` package. 

```r
df %>%
	select(any_of(var1, var2, var3))

```

this is useful if you are applying the same function to different datasets (maybe with a targets pipeline or just a purrr::map over many datasets) and these datasets contain different variable names (works great if the same variable is named differently on each dataset, which is great for messy data.)



### Remove rows where any of multiple columns contains a NA. 

```r
my_data[complete.cases(my_data[,c("x2","x3")]),]
```


### Remove rows where at least 1 column contains a NA. 

```
df %>% drop_na

```

### Check amount of NAs in a column

```r
sum(is.na(dataset$variable))

```



### Select columns that match multiple stings
```
data  <- read_csv(path_to_data) %>%
    select(matches("acc|mag|pitch|roll"))
```
