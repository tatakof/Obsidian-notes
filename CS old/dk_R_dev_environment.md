from r_dev_projects

## Pre-requisites


-   Install Docker for your particular OS. For my development setup, it is Ubuntu 20.04. Instructions can be found at [docs.docker.com/get-docker](https://docs.docker.com/get-docker/)
    -   If you are using a Linux-based operating system: Ensure that your user ID is added to the `docker` group.
-   Install Visual Studio Code. Downloads and more information can be found at [code.visualstudio.com](https://code.visualstudio.com/)
Go to VSCode extensions (left bar, Ctrl+Shift+X) 

- Install remote development extension pack

![[Pasted image 20220403172606.png]]

-----------------------------------------------------------------------

Visual Studio Code Remote Development Extension Pack

The **Remote Development** extension pack allows you to open any folder in a container, on a remote machine, or in the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl) and take advantage of VS Code's full feature set. Since this lets you set up a full-time development environment anywhere, you can:

-   Develop on the same operating system you deploy to or use larger, faster, or more specialized hardware than your local machine.
-   Quickly swap between different, separate development environments and make updates without worrying about impacting your local machine.
-   Help new team members / contributors get productive quickly with easily spun up, consistent development containers.
-   Take advantage of a Linux based tool-chain right from the comfort of Windows from a full-featured development tool.

No source code needs to be on your local machine to gain these benefits since Remote Development runs commands and extensions directly on the remote machine.
-   **[Remote - SSH](https://aka.ms/vscode-remote/download/ssh)** - Work with source code in any location by opening folders on a remote machine/VM using SSH. Supports x86_64, ARMv7l (AArch32), and ARMv8l (AArch64) glibc-based Linux, Windows 10/Server (1803+), and macOS 10.14+ (Mojave) SSH hosts.
-   **[Remote - Containers](https://aka.ms/vscode-remote/download/containers)** - Work with a separate toolchain or container based application by opening any folder mounted into or inside a container.
-   **[Remote - WSL](https://aka.ms/vscode-remote/download/wsl)** - Get a Linux-powered development experience from the comfort of Windows by opening any folder in the Windows Subsystem for Linux.
---------------------------------------------------------------------

-   Install the [Docker Extension Pack](https://marketplace.visualstudio.com/items?itemName=formulahendry.docker-extension-pack) (while not necessarily required, I find it very useful for managing my containers inside the IDE)

![[Pasted image 20220403172858.png]]
-   If you use SSH keys with your online code repository account (for example GitHub or GitLab) you need to share your key with containers built. The process is documented at on the VSCode docs [here](https://code.visualstudio.com/docs/remote/containers#_sharing-git-credentials-with-your-container). For my setup, I have to run this once before launching VSCode: `ssh-add ~/.ssh/{name_of_key}`. I have a custom key but I would imagine most users will have a default key name of `id_rsa`.


## VSCode setup
The `.devcontainer` directory in this repository contains the custom configuration files and build instructions for creating the development container. The `Dockerfile` and `devcontainer.json` were adapted from the VSCode dev containers GitHub repository [here](https://github.com/microsoft/vscode-dev-containers/tree/master/containers/r). Highlights of the customizations I made:

-   Use the base Docker image of `rocker/r-ver:4.0.2` from the [Rocker Project](https://www.rocker-project.org/)
-   Install the [Fish](https://fishshell.com/) shell instead of [ZSH](http://zsh.sourceforge.net/)
-   Install additional OS libraries to make installation of R package binaries relatively painless
-   Install the [radian](https://github.com/randy3k/radian) alternative R console
-   Install `renv`
-   Install certain dotnet core runtime packages (this may not be necessary in future)
-   Configure environment variables for custom location of `renv` cache directory mounted into the container
-   Set the default user as my user account and not root.



## Configuring a central package cache
I have set up a local directory on my system that is mounted as a volume in each container to hold the R package cache. As long as your logged-in user has read and write priveleges to this directory on your host system, there should be no issues with each container reading and writing to the cache dir. In the containers, the directory is located at `/renv/cache` while on my host system it is located at `/opt/local/renv/cache`, but this could be any directory on your host system. In the Docker configuration files for each container, I set up the following environment variables:

```
RENV_PATHS_CACHE_HOST=/opt/local/renv/cache
RENV_PATHS_CACHE_CONTAINER=/renv/cache
RENV_PATHS_CACHE=/renv/cache
```



## Using Renv with VS-Code

One (intentional) effect of using `renv` is that out of the box the project's package library will not link to packages in the default library that are not included in the base installation of R. The interactions between an R session and VS-Code are largely driven by the [`{launguageserver}`](https://github.com/REditorSupport/languageserver) package available on CRAN. My solution to ensure any project with `renv` enabled can use all of the same integrations with VS-Code is to create a custom `.Rprofile` that contains certain triggers to bootstrap the installation of `languageserver` and perform necessary environment configurations if the session detects that the `TERM_PROGRAM` environment variable is set to `vscode`. The file [`.devcontainer/library-scripts/.Rprofile-vscode`](https://github.com/rpodcast/r_dev_projects/blob/master/.devcontainer/library-scripts/.Rprofile-vscode) is automatically copied to the container's `renv` cache directory, and can be manually copied to overwrite the current project's `.Rprofile` file. Much of this solution was adapted from ideas discussed in issue [vscode-R/259](https://github.com/Ikuyadeu/vscode-R/issues/259). The contents are below:

```
# setup if using with vscode and R plugin
if (Sys.getenv("TERM_PROGRAM") == "vscode") {
    source(file.path(Sys.getenv(if (.Platform$OS.type == "windows") "USERPROFILE" else "HOME"), ".vscode-R", "init.R"))
}
source("renv/activate.R")

if (Sys.getenv("TERM_PROGRAM") == "vscode") {
    # obtain list of packages in renv library currently
    project <- renv:::renv_project_resolve(NULL)
    lib_packages <- names(unclass(renv:::renv_diagnostics_packages_library(project))$Packages)

    # detect whether key packages are already installed
    # was: !require("languageserver")
    if (!"languageserver" %in% lib_packages) {
        message("installing languageserver package")
        renv::install("languageserver")
    }
    
    if (!"httpgd" %in% lib_packages) {
        message("installing httpgd package")
        renv::install("nx10/httpgd")
    }

    if (!"vscDebugger %in% lib_packages) {
        message("installation vscDebugger package")
        renv::install("ManuelHentschel/vscDebugger@v0.4.3")
    }

    # use the new httpgd plotting device
    options(vsc.plot = FALSE)
    options(device = function(...) {
      httpgd::httpgd()
      .vsc.browser(httpgd::httpgdURL(), viewer = "Beside")
    })
}
```
















from: https://santhoshsundar.medium.com/building-container-based-development-environment-with-visual-studio-code-2d7111c650bd

One of the challenges when setting up the local development environment for your team is ensuring that all developers have a setup that is either same or meets the requirements. The traditional approach to this problem is to lay down onboarding guidelines and expect developers to follow them. However, from version compatibility issues to individual’s experience to not using the right tools, there are varying hurdles to achieve uniformity in setting up the environment.

![](https://miro.medium.com/max/1082/1*jEj-6le5VzTy0H-EkFCqaA.png)



An alternative solution is a development environment pre-configured with all the required libraries and dependencies that developers can spin-off in a container. Developers can then work inside the isolated environment the container offers. This drastically minimizes the time a developer spends between cloning the codebase to begin working on it.


![](https://miro.medium.com/max/1202/1*k1Vl_mAIa029GrDkf5hUdw.png)

In addition to providing the same environment to all developers, we can facilitate the same set of tools, extensions, and even the theme in Visual Studio Code. Though this is optional, we can leverage this to automatically install specific extensions that your project requires. This can avoid inconsistent use of tooling and as well stop bothering developers to install them manually.



Setup: 

Install docker and remote -- containers
Go to your project and create a folder named `.devcontainer` in the root directory of your project. This new folder holds the configuration files required for the development container. 

Copy and paste the **Dockerfile** and **devcontainer.json** inside the .devcontainer folder.

Once done, we need to build the container. TO do this, either use "Open Folder in Container" or "Reopen in Container" from the VS Code command palette (Ctrl+Shift+P)
![[Pasted image 20220403174646.png]]


The build and configuration of the container is a one-time activity and takes time. Subsequent rebuilds are faster if there are no changes. But if there ais a change in `devcontainer.json` or the `Dockerfile`, a rebuild id required to apply the changes. You will be prompted to rebuild if you try to reopen directly. 

If you exit the container or VS Code, you can get back into the container using the option ‘Reopen in Container” This will spin up the container that was already configured and just starts the development server again. If VS Code finds the .devcontainer configuration in a codebase, it automatically prompts you to start the container.

![[Pasted image 20220403175559.png]]

## **A few other benefits:**

-   The file system between the container and your local machine is in sync, so you can access your changes in either environment.
-   You could run as many applications that require a different version of dependencies without installing or modifying any on your computer.
-   Anyone in your team can run the application on their computer to code, review or play around, including non-technical members.
-   Runs agnostic of the operating system.

-   The VS Code terminal lets you run any scripts or commands since it is already in the container’s workspace. But if you want to use other tools such as the “Terminal” of macOS, you need to find the container and then perform [docker exec](https://docs.docker.com/engine/reference/commandline/exec/).
![](https://miro.medium.com/max/1400/1*IfgGEW9h5mj2GVb9YQ-p6Q.png)
-   Since the application is running inside a Docker container, it will have access to a limited resource (CPU, Memory, Swap, etc). In most cases, the default limit should be fine. However, depending on your application, you may need to increase them in the Docker preferences to avoid lags.

![](https://miro.medium.com/max/1400/1*PJ2gRlhGtZa2oR-zmtjq6g.png)
