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
	withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '<CREDENTIAL_ID>', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
		sh 'echo uname=$USERNAME pwd=$PASSWORD'
		echo 'Push imagen al docker hub'
		sh 'docker login -u $USERNAME -p $PASSWORD'
		sh 'docker push manuexcd/spring-cloud-discovery'
		sh 'docker rmi spring-cloud-discovery:latest'
		sh 'docker rmi manuexcd/spring-cloud-discovery:latest'
	}
}