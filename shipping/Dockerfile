
FROM  maven:3.9.11 AS build
EXPOSE 8080
WORKDIR /opt/server
COPY pom.xml  .
COPY src ./src
RUN mvn clean package 
RUN mv target/shipping-1.0.jar shipping.jar

FROM eclipse-temurin:21-jre-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build  /opt/server /opt/server
EXPOSE 8080
LABEL com.project:"roboshop" \
      component:"shipping" \
      created_by:"balachandra"
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql
 CMD ["java","-jar","shipping.jar"]



# FROM maven:3.9.11
# EXPOSE 8080
# WORKDIR /opt/server
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar
# ENV CART_ENDPOINT=cart:8080 \
#     DB_HOST=mysql
# CMD ["java","-jar","shipping.jar"]
