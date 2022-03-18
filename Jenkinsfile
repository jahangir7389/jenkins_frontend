pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build') {
			steps {
				dir('jenkins_frontend'){
					sh 'docker build -t jahangir7389/test-frontend-app .'
				}
			} 
		}
    stage('Test') {
      steps {
			dir('jenkins_frontend'){
				sh 'docker container run --rm -p 8001:8080 --name node -d jahangir7389/test-frontend-app ' 
				sh 'sleep 5'
				sh 'curl -I http://localhost:8001'
			}
		} 
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push jahangir7389/test-frontend-app:latest'
					} 
				}
			} 
		}
	}
}
