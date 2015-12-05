####Dockerfile
A text document that contains all the necessary commands to create a docker image.<br>
Dockerfile + context ---**docker build**---\> docker image<br>
Context: **PATH** (local filesystem) or **URL** (git repo). The context is processed recursively.<br>
Usage: `docker build [OPTIONS] PATH | URL`<br>
Use .dockerignore file to exclude files/folders.<br>
By default the `Dockerfile` should be at the root of the context.<br>

Basic format:<br>
\# **Comment**<br>
INSTRUCTION arguments

####INSTRUCTIONS
* **FROM**<br>Specifies the base image.<br>**FROM java:8**
* **ENV**<br>Sets an environment variable<br>**ENV mypath /usr/bin**<br>Can be referenced as $mypath<br>

####Sources
* https://docs.docker.com/engine/reference/builder
