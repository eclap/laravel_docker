# Quick Laravel Setup Using Docker

## Description

This is a quick way to setup Laravel using Docker. 
This is useful for use cases like experimentation or tutorials where you just want to have a running Laravel immediately.

Notes: 
- I am new at Docker so expect that this would change as I learn more optimum practices.
- This is heavily based from this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-containerize-a-laravel-application-for-development-with-docker-compose-on-ubuntu-18-04). If you want more explanations and descriptions, refer to that tutorial. The focus of this writeup is just to present the barebone actual step-by-step to start using Laravel with Docker.

## Requirements
- [Docker](https://www.docker.com)
- [Git](https://git-scm.com/)

## Setup

#### STEP 1
Fetch the codebase in Github.
```
git clone git@github.com:eclap/laravel_docker.git
cd laravel_docker
```

#### STEP 2
Install dependencies using Composer.
```
cd src
docker  run --rm -v $(pwd):/app composer install
cd ..
```

#### STEP 3
Setup .env files from .env.example. 
Two .env files are needed, one is in the root folder, and the other is in the "src" folder.
This is a temporary setup as I'm still figuring out an issue in just having one ".env" file.
So assuming that .env.example files have the correct values already:
```
cp .env.example .env
cp src/.env.example src/.env
```

#### STEP 4
Run the docker build command.
```
docker-compose build app
```

#### STEP 5
Start the docker container.
```
docker-compose up -d
```

#### STEP 6
After "step 5" Laravel homepage should be available in http://localhost:8001.

#### STEP 7
Run artisan commands.
```
docker-compose exec app bash
php artisan key:generate
php artisan migrate
php artisan db:seed
exit
```
