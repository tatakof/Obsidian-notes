From https://environments.rstudio.com/upgrades.html

## Snapshot and Restore for Upgrades



The first concern for safe upgrades is project isolation. By isolating projects, you can ensure that upgrading the packages for one project won’t break code in other projects. This type of isolation is accomplished by creating per-project libraries. The `renv` package [[package_Renv]] makes this easy. Inside of your R project, simply use:

```clike
# inside the project directory
renv::init()

# check to see the isolated project library
.libPaths()
```

The next concern for safely upgrading packages is creating a safety net. If the package upgrade goes poorly, you’ll be able to revert the changes and return to a working state. Again, the `renv` package [[package_Renv]]  makes this process easy.

```clike
# record the current dependencies in a file called renv.lock
renv::snapshot()
# commit the lockfile alongside your code in version control
```

With an isolated project and a safety net in place, you can now proceed to upgrade or add new packages, while remaining certain the current functional environment is still reproducible. The [`pak` package](https://github.com/r-lib/pak) can be used to install and upgrade packages in an interactive environment:

```clike
# upgrade packages quickly and safely
pak::pkg_install("ggplot2")

# the interactive prompt shows you exactly what will change
# helping avoid unintentional or surprising changes
```

If the process of upgrading packages goes poorly, you can roll back the change using the safety net created earlier:

```clike
# use this function to view the history of your lockfile
renv::history()

# if an upgrade goes astray, revert the lockfile
renv::revert(commit = "abc123")

# and restore the previous environment
renv::restore()
```

The safety net provided by the `renv` package [[package_Renv]] relies on access to older versions of R packages. For public packages, CRAN provides these older versions in the [CRAN archive](https://cran.rstudio.com/src/contrib/Archive). Organizations can use tools like [RStudio Package Manager](https://rstudio.com/products/package-manager) to make multiple versions of private packages available






