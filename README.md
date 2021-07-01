# General

## Deployment type

Docker

## Image

Based on: https://hub.docker.com/r/rocker/rstudio

## Licence

AGPL v3

## Version

4.1.0

## Description

RStudio Web Server is a Linux server application that provides a web browser/based interface to the version of R running on the server. Deploying R and RStudio on a server has a number of benefits: the ability to access R workspace from any computer at any location; sharing of code, data, and other files with colleagues; allowing multiple users to share access to the more powerful computing resources available on a server; control access to data in a centralized manner; centralized installation and configuration of R, R packages and other libraries.

RStudio is an integrated development environment for R and Python, with a console and a web-based graphical interface, syntax-highlighting editor that supports direct code execution, and tools for plotting, debugging and workspace management. The RStudio reference architecture proposes to provide a general r developer environment with integrated data management and tools that can help the development process. In this stack, we created an RStudio manifest with the data management part.

# Deployment

A. General example:

```sh
docker run -d --rm \
        --name rstudio \
        -e PASSWORD=rstudio \
        -p 8787:8787 \
        -v $HOME/rstudio/data:/home/rstudio \
        rocker/rstudio:4.1.0
```

## Parameters

|Name|Value|Description|
|-|-|-|
|Port|`-p 8787:8787`|JupyterLab WebGUI|
|Volume|`$HOME/rstudio/data:/home/rstudio`|Persist rstudio data|
|Envs|`-e USER=<CUSTOM_NAME>`<br/>`-e USERID=<UID>`<br/>`-e GROUPID=<GID>`<br/>`-e UMASK=022`<br/>`-e PASSWORD=rstudio`<br/>`-e ROOT=TRUE`|Define custom user name<br/>Define custom user id<br/>Define custom group id<br/>Define custom umask<br/>Define RStudio password<br/>Give the user root permissions (add to sudoers)|

<br/>

Custom uid/gid etc is usually only needed when sharing a local volume for a user/group whose id does not match the default (1000:1000). Failing to do this could make files change permissions on the linked volume when accessed from RStudio.

## Testing

Direct your browser at: [http://\<HOST\>:8787](http://<HOST>:8787) and log in with username `rstudio` and the password you set.

# Authentication

The WebUIs are protected by password. The default password is "rstudio", which can be changed with `PASSWORD` enviroment variable.

# Reference

https://docs.rstudio.com/
