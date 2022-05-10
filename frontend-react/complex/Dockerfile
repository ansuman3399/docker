#Prod file
#Dockerizing the react app.
#To build this use: docker build -f Dockerfile.dev ansumanm20/react-docker-app:0.0.1.release 
FROM node:16-alpine
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY  . .
CMD [ "npm","run","start" ]