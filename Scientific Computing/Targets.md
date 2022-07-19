### Git
The entire `_targets/` data store should generally not be committed to Git because of its large size.

However, you may wish to commit `_targets/meta/meta`, which is critical to checking the status of each target and reading targets into memory.


## Only run one or some targets
https://books.ropensci.org/targets/dynamic.html#dynamic-branching-performance

```
tar_make(names = "target name")
```