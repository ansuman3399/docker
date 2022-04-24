#Specify the base image
FROM node:alpine

#Creating default working directory
WORKDIR /usr/app

#Copy application data to the intermediate container root folder in order to make the index.js and package.json available 
COPY ./package.json ./

#install some dependencies
RUN npm install

#Copy other application files after npm isntall to reduce cache busting and unnecessary rebuilds
COPY ./ ./

#Default command
CMD ["npm","start"]