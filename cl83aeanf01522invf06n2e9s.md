## What is Docker? Beginner friendly

## Software Development Lifecycle
Before learning about Docker, let's discuss Little bit about Software Development Lifecycle to understand the need and position of Docker in Software Developer 

Software Development can be divided into mostly 2 parts. One is Development, another one is Operations.

- Development mostly has writing Code, testing the Code, and also debugging it.

- Operations, on the other hand, is mostly deploying the Code into a server and monitoring its performance.


![SDLC](https://cdn.hashnode.com/res/hashnode/image/upload/v1661776599808/ZSO2o41S1.jpg align="center")

When we write the application or software on our local machine, we set up an environment. The environment mostly has:

1. `Operating System` (Linux, Windows)
2. `Runtime`(Python, Node.Js)
3. `Package Manager` (Pip, NPM)
4. `Runtime dependencies` (NumPy, Django)

![Software Layers](https://cdn.hashnode.com/res/hashnode/image/upload/v1661447683111/ZPuTlvZ5I.webp align="center")

So, now to run the application on the server, we need to replicate all 4 layers to the server.

## So, What's the problem?

Having all these layers in place correctly with the correct versions is not a straightforward task. 

- We first need a well-suited `Operating System`, but what if we don't have permission to do so? What if we are using a cloud environment and can't change the OS?

- Once we have the correct OS set up, you need to install the proper `runtime and package manager`, but again we have to `well document` and perform the exact steps each and every time.

- Most dependencies now depend on the exact version of the `OS` and `Runtime`. The deps must be installed using a script such as `pip` or `npm`. Most of the time, it isn't so straightforward. A small change in the OS version or Runtime version can have a significant impact.

- Lastly, if you have all the environment set up, you have to place your source code or bundle into the proper location.

Also, any change in one step will impact all the other steps and we also have to replicate the same changes to all the deployments we have.

All these above tasks take a significant amount of development time.

So, if you are a `SOLO DEVELOPER`, get ready to spend a lot of time on individual deployment.

## How Docker helps?

Docker helps us to move the deployment from one place to another place with little or no hassle. 

> Using Docker we create `Images` or in simple words `Bundles` which have everything in place from the Operating System with the Runtime and also the Codebase.

We can use the Docker image to deploy the code at any Server, which has the docker runtime installed in it.

### What are Docker Container and Docker Image?

- **Container** - A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 

- **Image** - A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings.

## The Full Picture

With Docker, we can build and run multiple Applications on the same computer. Each has a separate Operating System, runtime, and libraries. All the apps are standalone and don't share any dependency with the underlying Infrastructure and other Apps as well. Containers isolate the application from its environment and ensure that it works uniformly despite differences for instance between development and staging.

![Container and Environment](https://cdn.hashnode.com/res/hashnode/image/upload/v1663259213746/gNGXzXnxp.webp align="left")

This is the magic of Docker. Although the Apps are on the same Infrastructure, sharing the same CPU, Memory, Disk, and IO, from the application's perspective, they all are running on separate Machines, all of which have different Operating Systems, runtimes, and libraries.

Each Container has its own File System, own Process IDs, own Network footprints like IP address.

## What is Docker Runtime and How to install it?

 The container runtime is the low-level component that comes with Docker that creates and runs containers. Docker currently uses `runC`, the most popular runtime, which adheres to the  [OCI standard](https://opencontainers.org/) that defines container image formats and execution.

Docker is available free on Docker's website. Docker support all the major Operating Systems. We can download it from https://docs.docker.com/get-docker/.

## Conclusion

This blog addresses the basic and theoretical perspective of Docker, and it's completely for beginners.

In the next blog, I'll address the docker building and running process.


Thanks for reading!!