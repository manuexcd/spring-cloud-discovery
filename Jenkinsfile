#!groovy

node {
   stage 'Docker image'
   echo 'Creando imagen de Docker'
   sh 'mvn clean package docker:build'
   
   stage 'Docker tag'
   echo 'Tag imagen'
   sh 'docker tag spring-cloud-discovery manuexcd/spring-cloud-discovery'
   
   stage 'Docker push'
   echo 'Push imagen al docker hub'
   sh 'docker push manuexcd/spring-cloud-discovery'
}