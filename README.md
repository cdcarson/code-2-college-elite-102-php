#  Docker LAMP Stack with VS Code Remote Container Support

Notes: this stack is for **educational and development purposes only**  -- it's not intended for production deployments. Forked and modified from https://github.com/sprintcube/docker-compose-lamp.


A basic LAMP stack environment built using Docker Compose, intended to be used with VS Code Remote Containers. 

It consists of the following:

- PHP
- Apache (a web server)
- MySQL (a relational database)
- phpMyAdmin (an admin app for looking at what's in your MySQL database)
- Redis (an in-memory data store/cache)
- Node (for js/css asset building)

##  Getting Started
 
### 1. Prerequisites

You should know how to open a Terminal on your OS. In Mac this app is called "Terminal."

You should make sure you have the following installed:
 - git: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git This will allow us to push and pull from GitHub.
- Docker Desktop: https://www.docker.com/products/docker-desktop This is the program that installs and runs the "containers" for our local dev environment: PHP, Apache, MySQL and so on. Each container is a "virtual" machine running Linux. Whats the point? Rather than each developer installing PHP, Apache, MySQL, etc. on their own local machine, everybody shares a stable, reproducible environment across operating systems and machines.
- VS Code: https://code.visualstudio.com/ This is the code editor the we'll be using.


### 2. Clone this repo and build the containers (Terminal)
Once you have those things installed, open up a terminal and clone this repo...
```bash
git clone git@github.com:cdcarson/lamp-docker-vscode.git
```
`cd` into the directory...
```bash 
cd lamp-docker-vscode
```

Copy `sample.env` to `.env`...
```bash 
cp sample.env .env
```

Build the containers...
```bash
docker-compose up -d
# You'll see a whole bunch of stuff going on here.
# It may take some time to complete. Sit back and relax.
```

The first time you run `docker-compose up` it may take a significant amount of time (like 5 or 10 minutes) to complete. Docker is downloading and compiling a whole bunch of source code. Don't worry -- the next time it'll only take a few seconds. You should see something like this at the end:

```bash
Creating lamp-dev-database ... done
Creating lamp-dev-redis    ... done
Creating lamp-dev-php73      ... done
Creating lamp-dev-phpmyadmin ... done
```

Make sure everything's good. Open up Docker Desktop. You should see the `lamp-dev` app running:

![Docker Desktop after docker-compose up -d](docs/img/docker-desktop-after-start.png)

Go to http://localhost:3100/. You should see a "Hello World" web page:

![The Web Page](docs/img/the-web-page.png)

You can click on the links on the page to make sure everything is working.

**Important before going on to the next step:** Shut everything down. In the terminal:
```bash
docker-compose down
```


### 2. Start VS Code and open the project as a dev container

Start VS Code. Open the `lamp-docker-vscode` folder.  `File -> Open Workspace...`.

If you do not already have the "Remote - Containers" VS Code plugin installed, you'll be prompted to install it:

![Install Prompt](docs/img/recommended-extensions-prompt.png)

Go ahead and click "Install."

You will then see a prompt to reopen the workspace in a dev container:

![Reopen in Container Prompt](docs/img/reopen-in-container.png)

Click "Reopen in Container." If you don't see this prompt, you can always open in via the [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette). Select "Reopen in Container":

![Reopen in Container from Command Pallete](docs/img/Reopen-in-container-command.png)

#### Wait for the containers to build.

If you've followed the steps above (i.e. running `docker-compose up` from the command line) it should only take a few seconds for the containers to boot. If not, it may take a few minutes to download and compile the source code.




