#Specify the base image
FROM node:alpine

#Copy application data to the intermediate container root folder in order to make the index.js and package.json available 
WORKDIR /usr/app
COPY ./ ./

#install some dependencies
RUN npm install

#Default command
CMD ["npm","start"]