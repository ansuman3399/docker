#Use existing docker image as base
FROM alpine

#Download and install dependency
RUN apk add --update redis

#Tell the image what to do when it start as a container
CMD [ "redis-server" ]