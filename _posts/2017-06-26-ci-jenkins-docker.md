---
title: Continuous Building and Testing with Jenkins (Blue Ocean) Pipelines and Docker
---

In this post, we will see how to run a Jenkins Blue Ocean continuous integration server using Docker for both the Jenkins application and the build/test environments. We will introduce the mechanics of Jenkins Declarative Pipelines and create a simple example, starting from an existing. 

In summary, we'll see: 

- How to deploy a Jenkins Blue Ocean application to manage Continuous Integration Pipelines
- How to configure a docker-based execution environment
- How to create a new pipeline using the Blue Ocean interface for an existing code repository
- How Pipeline-As-Code works using Jenkins Declarative Pipelines


### Continuous Integration (in 2017)

Continuous Integration is one of the main practices in the Extreme Programming landscape, although through the years it has transcended beyond XP to become one of the most common *cool things* to have in your development team. Due to the availability of numerous and versatile automation  tools (Jenkins, Travis, Go, AppVeyor, Bamboo ...), continuously building and testing your codebase is just one of those things rapidly becoming a *commodity* more than a rare thing or a luxury good in the software development world.

But continuous integration is much more than having an automation _gadget_ in place. The concept comes from the idea of constantly releasing internal versions of an whole system, with the aim to discover problems early and reveal design flaws. Kent Beck incorporated this idea, originally formulated by Grady Booch (*add footnote*), into his list of _practices_. The definition of continuous integration, as written in eXtreme Programming eXplained (1999) is the following:

>  Integrate and build the system many times a day, every time a task is completed.

While, again, this seems something common or quotidian in our present day, think about what it could mean twenty years ago. Now, incorporate the following thought: Cruise, the first CI tool, was released years after the C3 project concluded, and it wasn't nearly as functional as today's automation tools. This means in the early days of continuous integration, it wasn't about the tools... because _there were no tools_.

[buscar tweet retuiteado por XPSurgery sobre XP original]

In its essence, CI is more about integrating ideas and obtaining feedback. Overwhelmed and amazed by the shiny features of the latest automation _doohickey_, we sometimes forget that. _Communication_ and _Feedback_ are two of the four values of XP. And it is _people and interactions over processes and tools_, remember?

And when it comes to the tools, continuous integration does not begin with the automation provided by Jenkins or Travis. It definitely starts much earlier, when we put version control systems in place and share our changelists with the rest of the team as part of our daily work. Using git can be seen as the foundation for good continuous integration practice, and consequently, there has been a lot of effort lately in defining the correct workflows or _branching models_ when working with git repositories, and this is precisely motivated for the need of integrating changes the best way possible.

[caption para el tuit de lunivore y dan north sobre integración continua trunk, etc: while the "gitflow" branching model dominated the scene during the last years, many people advocate for a trunk-based model in which integration is not deferred/procrastinated but it is incentivated].

So, what makes it a good continuous integration? The moment we embrace the practice of sharing our ideas and our code with the rest of our team continuously, we are keeping the spirit of continuous integration. And of course we have abanico de herramientas disponibles para ello. 

Martin Fowler proponía su "CI certification test"



In which we commit several changes to the repository, and that triggers a pipeline. 

... and it's all there, in the repository: the Jenkinsfile contains all the _stages_ and _steps_ of our _build pipeline_. 

Once we have seen it, we can _rosebud_ to the beginning and see how surprisingly easy is to setup our CI server.

## Basic Setup: ubuntu and Docker

Our host machine is has a fresh Ubuntu 16.04 with Docker installed. We have created two users, jenkins and jenkins-agent. Why is that?

- `jenkins` is our main user, which will run the Jenkins application (using a Jenkins image). 
- `jenkins-agent ` will be the one _running_ the actual jobs, i.e. running our `build` and `test` steps in the specified environment.

### Launching the Jenkins Blue Ocean server using docker

We can pull the official Blue Ocean image (`jenkinsci/blueocean:lts`) to simply run our server as: 

```
docker run -p 8080:8080  -v jenkins_home:/var/jenkins_home jenkinsci/blueocean:lts
```

#### Creating our custom Jenkins Blue Ocean image (with some nice plugins)

What if we wanted to automate things as much as possible? Can we include some extra plugins in our Jenkins server without having to manually install them from the admin panel once it is running? Yes we can. 

## What now? 
Through this article, we have launched a very simple CI server which should suffice for a small team.
- Continuous Deployment
- Using K8S in declarative pipelines