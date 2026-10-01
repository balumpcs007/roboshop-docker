FROM node:20.19.5-alpine3.22 AS build
EXPOSE 8080
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.22
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build  /opt/server /opt/server
EXPOSE 8080
LABEL com.project:"roboshop" \
      component:"catalogue" \
      created_by:"balachandra"
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
ENV MONGO=true \
     MONGO_URL="mongodb://mongodb:27017/catalogue"
 CMD ["server.js"]
 ENTRYPOINT ["node"]







# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO=true \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]

