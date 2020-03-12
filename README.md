### Project Setup

# Install Create React App globally:
$ npm install -g create-react-app@3.0.1

# Generate a new app:
$ create-react-app quiz
$ cd quiz


### Docker Setup
Add a Dockerfile to the project root:

# base image
FROM node:12.2.0-alpine

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /app/package.json
RUN npm install --silent
RUN npm install react-scripts@3.0.1 -g --silent

# start app
CMD ["npm", "start"]

# Add a file
.dockerignore:
node_modules

# Build and tag the Docker image:
$ docker build -t quiz:dev .

### Start Container
$ docker run -v ${PWD}:/app -v /app/node_modules -p 3001:3000 --rm quiz:dev

*Build the image and fire up the container:
$ docker-compose up -d --build

*Stop Docker:
$ docker-compose stop

*Using same container
$docker attach ID