---
title: Continuous Integration with Jenkins (Blue Ocean) Pipelines and Docker
---

In this post, we will see how to run a Jenkins Blue Ocean continuous server using Docker for both the Jenkins application and the jenkins agents. We will introduce the mechanics of Jenkins Declarative Pipelines and run a couple examples. 



### A typical day in JenkinsLand
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