####Dockerfile
A text document that contains all the necessary commands to create a docker image.<br>
Dockerfile + context ---**docker build**---\> docker image<br>
Context: **PATH** (local filesystem) or **URL** (git repo). The context is processed recursively.<br>
Usage: `docker build [OPTIONS] PATH | URL`<br>
Use `.dockerignore` file to exclude files or folders. It basically works like `.gitignore`.<br>
By default the `Dockerfile` should be at the root of the context.<br>

Basic format:<br>
\# **Comment**<br>
INSTRUCTION arguments

####INSTRUCTIONS
* **FROM**<br>Specifies the base image.<br>**`FROM <image>:<tag>`** or **`FROM <image>@<digest>`**<br>`tag` or `digest` values are optional, by default `latest` is used.<br>**`FROM java:8`**
* **ENV**<br>Sets an environment variable. The value set will be available for all descendent Dockerfile commands.<br>**`ENV <key> <value>`**<br>`ENV mypath /usr/bin`<br>Can be referenced as $mypath or ${mypath}<br>**`${mypath:-/etc}`** means the value of mypath is used if present, otherwise /etc
* **RUN**<br>Executes a command.<br>**`RUN <command>`** or **`RUN ["executable", "param1", "param2"]`**<br>`RUN` instructions are layered -> cached.
* **CMD**<br>Provides defaults for an executing container.<br>It can include an executable, though if absent `ENTRYPOINT` must be specified.<br>Only one `CMD` can be specified<br>**`CMD ["executable", "param1", "param2"]`** or **`CMD command param1 param2`**<br>`CMD echo "Example"`
* **ADD**<br>Copies new files, directories or remote file URLs into the local filesystem of the container.<br>**`ADD <src> <dest>`**<br>`ADD *.txt /textfiles` (Adds all files with .txt extension to the container's filesystem under /textfiles<br>The `<src>` path must be inside the context of the build. If `<src>` is a directory, the entire content of it is copied. The directory itself is not copied, only the contents.<br>If the `<src>` parameter is an archive in a recognised compression format, it will be unpacked.
* **COPY**<br>Basically the same as `ADD`, but it does not accept urls nor extracts compressed files.
* **EXPOSE**<br>Informs Docker that the container listens on the declared ports at runtime.<br>**`EXPOSE <port> [<port> ...]`**<br>`EXPOSE 80 8080`
* **MAINTAINER**<br>Sets the `Author` of the image.
* **LABEL**<br>Adds metadata to an image. A label is a key-value pair. Multiple `LABEL`s are allowed in a Dockerfile<br>**`LABEL <key>=<value> <key>=<value> ...`**<br>˙LABEL version="0.1" description="Example"`
* 

####RUN vs CMD
* `RUN` actually runs a command and commits the result at build time.
* `ĊMD` does not execute anything at build time, but specifies the intended command for the image.

####Sources
* https://docs.docker.com/engine/reference/builder
