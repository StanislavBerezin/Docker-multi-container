FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx
EXPOSE 3000
# we are copying the file from nginx which is responsible for ports
# root and serving html
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# this is where we get the build file and designated location
COPY --from=builder /app/build /usr/share/nginx/html