# You Me and Docker 🐳

A simple basic introduction to Docker in node.js w express.js and redis

![Logo](https://logos-world.net/wp-content/uploads/2021/02/Docker-Logo-2015-2017.png)

## Creating a Node Image

In the project directory create a file name Dockerfile. This file will contain independent image 
layers. 

```
  FROM node:15
  WORKDIR /app  
  COPY package.json .
  RUN npm install
  COPY . ./
  EXPOSE 5000
  CMD [ "node", "index.js"]
```
Here every step is called image layer, in this image we have 5 layers. 

```
  FROM node:15

  => Here node is the image and :15 is the version
```
```
  WORKDIR /app 

  => Setting up the working directory => /app
  => /app exists in Node container
  => Hold all the application code
  => Run commads from this directory
```
```
  COPY package.json .

  => Copy package.json to the image 
  => the . reletively refering to the /app directory 
```
```
  RUN npm install

  => Installing dependencies from package.json
```
```
  COPY . ./

  => Coping source codes and files to the image
  => The first . refers everyfile of our app
  => And the 2nd part ./ refers, everything will be copied to /app directory
```

Port and initial command
```
  EXPOSE 5000

  => Refering our app will run on port 5000
```
```
  CMD [ "node", "index.js"]

  => The initial command that will run our container
  => Here, node index.js runs our app
```


# Building the Docker Container
```
  docker build -t Image_Name .
```

At the first build, It will run all the layers independently and install required dependencies but 
from the next build docker will use the cashed result of the layers, if the layers are unchanged. 
This provides better optimization.



## At the first build
Ruuning all the 5 layers

![App Screenshot](https://i.ibb.co/G5t5KbC/dc3.jpg)

## At the second build
Using cashed results of the 5 layers

![App Screenshot](https://i.ibb.co/yn1NStg/dc2.png)

## List of all images
```
    docker image ls
    => Currently Running
```


## Deleting an Image
```
    docker image rm IMAGE ID>
```


## Running/deploying an Image
```
    docker run -p 4000:5000 -v LocalmachinePath:ContainerPath:ro -v /app/node_modules --env-file ./.env -d --name Container_Name IMAGE_Name
```

=> -d for detouching our container from the CLI 
=> --name Container_Name for giving this container a name
=> IMAGE_Name is the name of the image, we want to run
=> -v LocalmachinePath:ContainerPath is for Bind Mount. 
    Bind mount is a   volume that helps to sync local repo 
    with the docker container that gives the advantage of not
    deploying our container every time, we change something on 
    our file/code. :ro stands for read only file system. If you want 
    a read, write, edit and delete only file system, remove :ro from there.
=> -v /app/node_modules is for avoiding over writing node_modules file
=> --env-file ./.env is for environment variables. .env is the name
    of the file that holds all our env var in our project directory 
=> -p 4000:5000, the 5000 refering that our app is running on port 
    5000 and the 4000 (Can be any valid port number) means, if any 
    request comes to the port 4000, the request will be forwarded to
    the Docker container

![App Screenshot](https://i.ibb.co/LRPxnbT/dc4.png)

## List of running containers
```
    docker ps
```
```
    docker ps -a
    => All containers (Deleted/Running)
```

## Info of a container
```
  docker logs Container_name
```

## Deleting a container
```
    docker rm Container_Name -f
```

## Accessing to the docker container
```
  docker exec -it Container_Name bash
  => it for interactice mode
  => bash for viewing the file system
```

```
  ls 
  => To view all the files
```

```
  cat file_Name 
  => Viewing content of the file
```

```
  exit
  => For exiting from the directory
```

## Limiting files from the container
Just like .gitignore(avoid files to be pushed 
into our git repo) docker has .dockerignore file.
Works same as .gitignore, we need specify file 
name to the .dockerignore file 

