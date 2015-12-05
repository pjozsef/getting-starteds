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
* **ARG**<br>Defines a variable that is passed at build-time with the `docker build --build-arg <varname>=<value>` command. An environment variable with the same name hides the arg variable.<br>**`ARG <name>[=<default value>]`**<br>`ARG buildno`<br>`ARG user=admin`<br>Build-in arg variables: `HTTP_PROXY`, `HTTPS_PROXY`, `FTP_PROXY`, `NO_PROXY`
* **RUN**<br>Executes a command.<br>**`RUN <command>`** or **`RUN ["executable", "param1", "param2"]`**<br>`RUN` instructions are layered -> cached.
* **ENTRYPOINT**<br>Configures the container that will run as an executable. Only the last `ENTRYPOINT` takes effect. Command line arguments to `docker run <image>` will be arguments to `ENTRYPOINT`.<br>**`ENTRYPOINT ["executable", "param1", "param2"`** or **`ENTRYPOINT command param1 param2`**<br>`ENTRYPOINT ["top", "-b"]` (when `docker run -H` is called, `top -b -H` will start in the container)<br>The provided entry point setting can be overriden in `docker run` with `--entrypoint`.
* **CMD**<br>Provides defaults for an executing container.<br>It can include an executable, though if absent `ENTRYPOINT` must be specified. Command line arguments to `docker run <image>` will override `CMD`.<br>Only the last `CMD` takes effect.<br>**`CMD ["executable", "param1", "param2"]`** or **`CMD command param1 param2`**<br>`CMD ["--help"]` (passes `--help` to the executable if no `docker run` arguments were provided.
* **ADD**<br>Copies new files, directories or remote file URLs into the local filesystem of the container.<br>**`ADD <src> <dest>`**<br>`ADD *.txt /textfiles` (Adds all files with .txt extension to the container's filesystem under /textfiles<br>The `<src>` path must be inside the context of the build. If `<src>` is a directory, the entire content of it is copied. The directory itself is not copied, only the contents.<br>If the `<src>` parameter is an archive in a recognised compression format, it will be unpacked.
* **COPY**<br>Basically the same as `ADD`, but it does not accept urls nor extracts compressed files. It is the preferred instructicon over `ADD`.
* **EXPOSE**<br>Informs Docker that the container listens on the declared ports at runtime.<br>**`EXPOSE <port> [<port> ...]`**<br>`EXPOSE 80 8080`
* **VOLUME**<br>Creates a mount point and marks it as holding externally mounted volumes from either the native host or other containers.<br>**`VOLUME <mountpoint> <mountpoint>...`**<br>`VOLUME /var/log /var/db`<br>
* **USER**<br>Sets the UID to use when running the image and when executing `RUN`, `CMD` or `ENTRYPOINT`.<br>**`USER <username>`**<br>`USER admin`
* **WORKDIR**<br>Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` or `ADD` instructions. Can be used multiple times. Relative paths will respect the previously set working directory.<br>**`WORKDIR <directory>`**<br>`WORKDIR /usr`<br>`WORKDIR bin`<br>`ENV DIR example`<br>``WORKDIR $DIR<br>`RUN pwd`(result is /usr/bin/example)<br>
* **STOPSIGNAL**<br>Sets the system call signal that will be sent to the container to exit. It can be a valid unsigned number, like 9 for SIGKILL<br>**`STOPSIGNAL signal`**
* **MAINTAINER**<br>Sets the `Author` of the image.
* **LABEL**<br>Adds metadata to an image. A label is a key-value pair. Multiple `LABEL`s are allowed in a Dockerfile<br>**`LABEL <key>=<value> <key>=<value> ...`**<br>˙LABEL version="0.1" description="Example"`
* **ONBUILD**<br>Defines a trigger instruction which will be executed when the image is used as the base for another build. Useful if the image will be used as a base to build other images.

####RUN vs CMD
* `RUN` actually runs a command and commits the result at build time.
* `CMD` does not execute anything at build time, used when container starts.

####COPY vs ADD
* They are functionally similar, `COPY` only supports basic file copying, `ADD` has more features like tar extraction and remote URL support. The best use for add is auto-extracting tar files into the image.

####CMD vs ENTRYPOINT
* `CMD` provides defaults, which are not used if  `docker run` arguments were supplied.
* `ENTRYPOINT` provides the entrypoint to be executed. `docker run` arguments will not override `ENTRYPOINT` parameters, but they will be appended to it.

####ARG vs ENV
* `ENV` is always persisted and set in the `Dockerfile`.
* `ARG` values come from the `docker build` command, they might not be set.
* Interaction between `ARG` and `ENV`:<br>`ARG USER_TYPE`<br>`ENV USER_TYPE ${USER_TYPE:-admin}`<br>The command line argument is used if present, otherwise a defauld value is used for the environment variable which hides the arg variable.

####Sources
* https://docs.docker.com/engine/reference/builder
* https://docs.docker.com/engine/articles/dockerfile_best-practices
* http://crosbymichael.com/dockerfile-best-practices
