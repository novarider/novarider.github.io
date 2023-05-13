---
title: "My first experiences with devcontainers"
date: 2023-04-09T12:39:54+01:00
draft: false
---

After an update of Visual Studio Code in my workplace, I encountered an added functionality: Devcontainers. So I decided to read into the topic. This lead to solving some problems in my workplace, which were unconformable to work with until now, but weren't also that bad to start finding another solution for them.

Let's begin at the start of the story:

# What are development containers?

Development containers are, as the name suggests, containers which have the purpose to unify development experience.
I am using docker as the container hoster. So our docker containers contain development, code formatting, linting, compiling and building tools which are needed for the project, we are currently working on. 

This setup has the advantage that every developer, and interested reader of a repository, has all tool at hand which are needed to work with the provided code and use the same development environment.

# How is the development container shared with developers?

"All this only brings advantage if the development container is served with the repository, right?" you may think now, and you are correct. This was the part why I never worked with development containers until now. I discovered [containers.dev](https://containers.dev), a website which describes a file format, to describe development containers and their setup.
Now we have the possibility to create some files, add them to the repository and everyone who pulls the repository has the development container at hand. This also works with different versions of your software, as the development container can be versioned like every other file in your repository.

# How are you using development containers?

Until now, you basically know what a container is and how I share it with other people to generate the same developing experience. But I also described that I solved some smaller problems with it, which I hadn't a solution until now, so let's talk about this:
My company has coding guidelines and linting guidelines, like every company nowadays should have. It makes the code more readable and can help to prevent coding errors in advance. But we had the problem that we used a wiki to document them and had to manually set up the tools to activate formatting and linting.
Now we have the possibility to create a container with all the tools, but we could not get our guidelines from the wiki in an automated way. We had to change the place where we are hosting the guidelines and how we configure our tools, so I did the following:

- To automate this enforcement with devcontainers I created a repository with all the tool's configurations and made the repository public. This brings the advantage that I can pull the config files via shell into the devcontainer.
- After that, I created the base development container definition à la [containers.dev](https://containers.dev) and preinstalled the formatting and linting tools in a setup script. I choose the "postCreateCommand" lifecycle method, but there are some other which could fit better in different cases.
- Then I load via shell the config files, hosted in the earlier mentioned repository, into the development container and set up the tools to work together.

Now my base container is ready to work with and all other changes are project specific. For easy access to the base container, I added the container definition to the coding guidelines repository and created a shell script which copies all necessary files.
I now want to start a new project, I have an only three steps to take:

1. Create a new folder where the project lives in and enter it.
2. Run the mentioned shell script to copy the devontainer files into the folder.
3. Open the folder in VS Code and let the IDE build the container.

After that, my basic coding tool set is created and I can start coding the project.

# How do you add developing and building tools

To develop we need some tools, like compilers, linkers etc. Let's call them features of the development container. As they are pretty important for the development process, we can also define them in the container definition files. Also, there is a [list on containers.dev](https://containers.dev/features), which have many tools ready to use.

If you cannot find the tool you need, you have two possibilities:

- Create a new feature and make it available for others!
- Use the lifecycle commands and a script to install and configure the software you need.
