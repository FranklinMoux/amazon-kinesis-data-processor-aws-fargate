#
# Build stage
#
FROM public.ecr.aws/hotmart/pipeline-maven:3-jdk-11-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean package

#
# Package stage
#
FROM public.ecr.aws/rogii/openjdk:11-corretto
COPY --from=build /home/app/target/producer-0.0.1-SNAPSHOT.jar /usr/local/lib/dataprocessor-producer.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/local/lib/dataprocessor-producer.jar"]