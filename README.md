# You-Me-and-Docker

# Here every step is called image layer, in this image we have 4 layers
# Every time we build the image, docker uses the cashed result of the layer,
# if the layer is unchanged. This provides better  optimization.


# Here node is the image and :15 is the version
FROM node:15

# Setting up the working directory => /app
# /app exists in Node container
# Hold all the application code
# Run commads from this directory
WORKDIR /app 

# Copy package.json to the image 
# the . reletively refering to the /app directory 
COPY package.json .

# Installing dependencies from package.json
RUN npm install

# Coping source codes and files yo the image
# The first . refers everyfile of our app
# And the 2nd part ./ refers, everything will be copied to /app directory
COPY . ./

# Refering our app will run on port 5000
EXPOSE 5000

# The initial command that will run our container
# Here, node index.js runs our app
CMD [ "node", "index.js"]

# Building the Docker Container
docker build .