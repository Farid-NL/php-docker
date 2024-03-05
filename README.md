<br/>
<p align="center">
  <a href="https://github.com/Farid-NL/php-docker">
    <img src="https://upload.wikimedia.org/wikipedia/commons/2/27/PHP-logo.svg" alt="Logo" height="80">
  </a>

  <h1 align="center">PHP Skeleton</h1>

  <p align="center">
    PHP development environment and project skeleton with docker.
  </p>
</p>
<br/>
<div align="center">

  <a href="">![Contributors](https://img.shields.io/github/contributors/Farid-NL/php-docker?color=dark-green)</a>
  <a href="">![Forks](https://img.shields.io/github/forks/Farid-NL/php-docker?style=social)</a>
  <a href="">![Issues](https://img.shields.io/github/issues/Farid-NL/php-docker)</a>
  <a href="">![License](https://img.shields.io/github/license/Farid-NL/php-docker)</a>

</div>


## Table Of Contents

- [About the Project](#about-the-project)
- [Prerequisites](#prerequisites)
- [Usage](#usage)

## About The Project

This repository tries to facilitate the setup of the development environment of PHP applications that doesn't require a framework.

## Prerequisites

You'll need Docker, whether the desktop version or the engine.

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Docker Engine](https://docs.docker.com/engine/install/)

Follow the instructions of your OS

## Usage

1. Clone the repo in the desired directory

    ```shell
    cd my-dev-dir/php-projects
    git clone git@github.com:Farid-NL/php-docker.git
    ```

2. Make a copy of `.env.example` called `.env`

    ```shell
    cp .env.example .env
    ```

3. Run the containers

    ```shell
    # Run on terminal   
    docker compose up

    # Run in detached mode 
    docker compose up -d
    ```

You can run commands inside the container with the help of `dev` script

```shell
# Show help message with command examples 
./dev help

# Install composer packages 
./dev composer install
```

## TODOs

- [ ] Explain how to add (modify) php and apache configurations
- [ ] Add a gif/video demo
- [ ] Make another branch for just apache + php skeleton
