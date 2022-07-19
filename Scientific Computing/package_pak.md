**pak**: A Fresh Approach to R Package Installation

pak installs R packages from CRAN, Bioconductor, GitHub, and local files and directories. It is an alternative to `install.packages()` and `devtools::install_github()`. pak is fast, safe and convenient.

[link](https://github.com/r-lib/pak)

## Why pak?

### [](https://github.com/r-lib/pak#fast)Fast

-   Fast downloads and HTTP queries. pak performs all HTTP requests concurrently.
    
-   Fast installs. pak builds and installs packages concurrently.
    
-   Metadata and package cache. pak caches package metadata and all downloaded packages locally. It does not download the same package files over and over again.
    
-   Lazy installation. pak only installs the packages that are really necessary for the installation. If the requested package and its dependencies are already installed, pak does nothing.
    

### [](https://github.com/r-lib/pak#safe)Safe

-   Private library (pak’s own package dependencies do not affect your regular package libraries and vice versa).
    
-   Every pak operation runs in a sub-process, and the packages are loaded from the private library. pak avoids loading packages from your regular package libraries. (These package files would be locked on some systems, and locked packages cannot be updated. pak does not load any package in the main process, except for pak itself).
    
-   To avoid updating locked packages, pak offers the choice of unloading them from the current R session, and/or killing other R sessions locking them.
    
-   Dependency solver. pak makes sure that you end up in a consistent, working state of dependencies. It finds conflicts up front, before attempting installation.
    

### [](https://github.com/r-lib/pak#convenient)Convenient

-   BioC packages. pak supports Bioconductor packages out of the box. It uses the Bioconductor version that is appropriate for your R version.
    
-   GitHub packages. pak supports GitHub packages out of the box. It also supports the `Remotes` entry in `DESCRIPTION` files, so that GitHub dependencies of GitHub packages will also get installed. See e.g. [https://cran.r-project.org/package=remotes/vignettes/dependencies.html](https://cran.r-project.org/package=remotes/vignettes/dependencies.html)
    
-   Easy time travel with [MRAN](https://mran.microsoft.com/timemachine) and [RSPM](https://packagemanager.rstudio.com/client/#/), to a specific date or when a certain R or package version was released.
    
-   Package sizes. For CRAN packages pak shows the total sizes of packages it needs to download.
    
-   Other package sources:
    
    -   local package files and directories,
    -   URLs to package files or package tree archives.