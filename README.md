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

##  Installation
 
### Prerequisites

You should know how to open a Terminal on your OS. In Mac this app is called "Terminal."

You should make sure you have the following installed:
 - git: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git This will allow us to push and pull from GitHub.
- Docker Desktop: https://www.docker.com/products/docker-desktop This is the program that installs and runs the "containers" for our local dev environment: PHP, Apache, MySQL and so on. Each container is a "virtual" machine running Linux. Whats the point? Rather than each developer installing PHP, Apache, MySQL, etc. on their own local machine, everybody shares a stable, reproducible environment across operating systems and machines.
- VS Code: https://code.visualstudio.com/ This is the code editor the we'll be using.


### Clone This Repo and Build the Docker Containers (Terminal)
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
# It'll take some time to complete. Sit back and relax.
```

The first time you run `docker-compose up` it will take a significant amount of time (like 5 or 10 minutes) to complete. Docker is downloading and compiling a whole bunch of source code. Don't worry -- the next time it'll only take a few seconds. You should see something like this at the end:

```bash
Creating lamp-dev-database ... done
Creating lamp-dev-redis    ... done
Creating lamp-dev-php73      ... done
Creating lamp-dev-phpmyadmin ... done
```

Open up Docker Desktop. You should see the app running:
![Docker Desktop after docker-compose up -d](docs/img/docker-desktop-after-start.png)




### Start VS Code and Reopen the Project as a Dev Container

Start VS Code. Open the `code-2-college-elite-102-php` folder.  `File -> Open Workspace...`.

If you do not already have the "Remote - Containers" VS Code plugin installed, you'll be prompted to install it:

![Install Prompt](docs/img/recommended-extensions-prompt.png)

Go ahead and click "Install."

You will then see a prompt to reopen the workspace in a dev container:

![Reopen in Container Prompt](docs/img/reopen-in-container.png)

Click "Reopen in Container." If you don's see this prompt, you can always open in via the [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette). Select "Reopen in Container":

![Reopen in Container from Command Pallete](docs/img/Reopen-in-container-command.png)

### Wait for the containers to build.


Your LAMP stack is now ready!! You can access it via `http://localhost`.

##  Configuration and Usage

### General Information 
This Docker Stack is build for local development and not for production usage.

### Configuration
This package comes with default configuration options. You can modify them by creating `.env` file in your root directory.
To make it easy, just copy the content from `sample.env` file and update the environment variable values as per your need.

### Configuration Variables
There are following configuration variables available and you can customize them by overwritting in your own `.env` file.

---
#### PHP
---
_**PHPVERSION**_
Is used to specify which PHP Version you want to use. Defaults always to latest PHP Version. 

_**PHP_INI**_
Define your custom `php.ini` modification to meet your requirments. 

---
#### Apache 
---

_**DOCUMENT_ROOT**_

It is a document root for Apache server. The default value for this is `./www`. All your sites will go here and will be synced automatically.

_**APACHE_DOCUMENT_ROOT**_

Apache config file value. The default value for this is /var/www/html.

_**VHOSTS_DIR**_

This is for virtual hosts. The default value for this is `./config/vhosts`. You can place your virtual hosts conf files here.

> Make sure you add an entry to your system's `hosts` file for each virtual host.

_**APACHE_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/apache2`.

---
#### Database
---

_**DATABASE**_
Define which MySQL or MariaDB Version you would like to use. 

_**MYSQL_DATA_DIR**_

This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.

_**MYSQL_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/mysql`.

## Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

* rewrite
* headers

> If you want to enable more modules, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

#### Connect via SSH

You can connect to web server using `docker-compose exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker-compose exec webserver bash
```

## PHP

The installed version of depends on your `.env`file. 

#### Extensions

By default following extensions are installed. 
May differ for PHP Verions <7.x.x

* mysqli
* pdo_sqlite
* pdo_mysql
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> If you want to install more extension, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if it seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

## phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

http://localhost:8080/  
username: root  
password: tiger

## Redis

It comes with Redis. It runs on default port `6379`.

## Contributing
We are happy if you want to create a pull request or help people with their issues. If you want to create a PR, please remember that this stack is not built for production usage, and changes should good for general purpose and not overspecialized. 
> Please note that we simplified the project structure from several branches for each php version, to one centralized master branch.  Please create your PR against master branch. 
> 
Thank you! 

## Why you shouldn't use this stack unmodified in production
We want to empower developers to quickly create creative Applications. Therefore we are providing an easy to set up a local development environment for several different Frameworks and PHP Versions. 
In Production you should modify at a minimum the following subjects:

* php handler: mod_php=> php-fpm
* secure mysql users with proper source IP limitations
