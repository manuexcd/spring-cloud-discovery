#!groovy

pipeline {
	environment {
		DOCKER_HOST='tcp://127.0.0.1:4243'
		registry = 'manuexcd/spring-cloud-discovery'
    	registryCredential = 'dockerhub'
	}

	agent any
	stages {
		stage 'Docker image' {
			steps {
				echo 'Creando imagen de Docker'
				sh 'mvn clean package docker:build'
			}
		}
		stage 'Docker tag' {
			steps {
				echo 'Tag imagen'
				sh 'docker tag spring-cloud-discovery manuexcd/spring-cloud-discovery'
			}
		}
		stage 'Docker push' {
			steps {
				script {
					docker.withRegistry( ‘’, registryCredential ) {
						echo 'Push imagen al docker hub'
						sh 'docker push manuexcd/spring-cloud-discovery'
						sh 'docker rmi spring-cloud-discovery:latest'
						sh 'docker rmi manuexcd/spring-cloud-discovery:latest'
					}
				}
			}
		}
	}
}