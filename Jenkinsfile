#!groovy

node {
	environment {
		DOCKER_HOST='tcp://127.0.0.1:4243'
		registry = 'manuexcd/spring-cloud-discovery'
    	registryCredential = 'dockerhub'
	}

	stage 'Docker image'
	echo 'Creando imagen de Docker'
	sh 'mvn clean package docker:build'
	
	stage 'Docker tag'
	echo 'Tag imagen'
	sh 'docker tag spring-cloud-discovery manuexcd/spring-cloud-discovery'
	
	stage 'Docker push'
	echo 'Push imagen al docker hub'
	sh 'docker login -u manuexcd -p xerezcd00'
	sh 'docker push manuexcd/spring-cloud-discovery'
	sh 'docker rmi spring-cloud-discovery:latest'
	sh 'docker rmi manuexcd/spring-cloud-discovery:latest'
}