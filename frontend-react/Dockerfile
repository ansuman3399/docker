FROM node:16-alpine as builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build
#build folder will be created inside the path /app/build

#Phase 2
#Nginx configuration
FROM nginx
EXPOSE 80
COPY --from=builder /app/build /usr/share/nginx/html
