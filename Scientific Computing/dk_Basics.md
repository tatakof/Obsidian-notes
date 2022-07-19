

From https://environments.rstudio.com/docker.html

In Docker, we have:

1.  **Dockerfile** - Describes the steps needed to create an environment. This is the recipe.
2.  **Image** - When you execute the steps in a Dockerfile, you _build_ the Dockerfile into an image which contains the environment you described. This is the batch of beer.
3.  **Registry** - Stores built images, so that others can use them. This is akin to a liquor store.
4.  **Container** - At a specific moment, you can _start_ a container from the image, which amounts to running a process in the built environment. This is drinking a pint from the batch of beer.

![[Pasted image 20211228230137.png]]




For R users and admins, it is important to understand that containers are tied to a process. This is the key difference in most user’s experience between a container and a virtual machine. For R users, the process that is running can fall into two buckets:


![[Pasted image 20211228230344.png]]

(In computer programming, an entry point is a **point in a program where the execution of a program begins, and where the program has access to command line arguments**. To start a program's execution, the loader or operating system passes control to its entry point.)


A data science container for R will contain six fundamental components:

1.  [Base Operating System](https://environments.rstudio.com/docker.html#base-operating-system)
2.  [System Dependencies](https://environments.rstudio.com/docker.html#system-dependencies)
3.  [R](https://environments.rstudio.com/docker.html#R)
4.  [R Packages](https://environments.rstudio.com/docker.html#r-packages)
5.  [Code](https://environments.rstudio.com/docker.html#code)
6.  [Data](https://environments.rstudio.com/docker/html#data)



Docker images can inherit and build off of one another, allowing these six components to be layers together to form a complete image that inherits components from earlier base images.

![[Pasted image 20211228230639.png]]



One reason Docker is so successful is because the different layers in a container are cached. In the example above, you can layer with code, without rebuilding the entire image. Only the steps “above” the code layer are re-run to create the updated image. The order of layers is very important, because it impacts the caching involved and the build time of the image.

In addition to caching, Docker images can build off of one another. As an example, the first 3 layers could be pulled into their own image:

IMAGE

Once the base image is saved, additional images could extend the base image by adding the top layers:

```bash
FROM company/base-r-image:3.5.2-xenial
RUN ...
```

The following sections will cover each component, with a special emphasis on reproducible environments.

Most Docker images start from a base operating system, the most common are versions of Ubuntu, CentOS, or Debian. These images are normally named by OS and tagged by release:

```bash
FROM ubuntu:xenial
```

```bash
FROM centos:centos6
```

This layer is the least likely to change, and is normally the “bottom” layer. For reproducibility, the Dockerfile should tag the desired release of the operating system.

### System Dependencies

R itself requires a number of system libraries in order to run, and a further set of system libraries are needed if the image will build R from source. See this section for [[]]