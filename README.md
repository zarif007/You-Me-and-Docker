
# You Me and Docker 🐳

A simple basic introduction to Docker in node.js




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

  => Coping source codes and files yo the image
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
  docker build .
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

