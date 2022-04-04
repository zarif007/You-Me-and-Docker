# You Me and Docker 🐳

A simple basic introduction to Docker in node.js

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
  docker build -t <Image Name> .
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
```

## Deleting an Image
```
    docker image rm <IMAGE ID>
```

## Running an Image
```
    docker run -p 4000:5000 -d --name <Container Name> <IMAGE Name>

    => -d for detouching our container from the CLI 
    => --name <Container Name> for giving this container a name
    => <IMAGE Name> is the name of the image, we want to run
    => -p 4000:5000, the 5000 refering that our app is running on port 
        5000 and the 4000 (Can be any valid port number) means, if any 
        request comes to the port 4000, the request will be forwarded to
        the Docker container
```
![App Screenshot](https://i.ibb.co/LRPxnbT/dc4.png)

## List of running containers
```
    docker ps
```

## Deleting a container
```
    docker rm <Container Name> -f
```
