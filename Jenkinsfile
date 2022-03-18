pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build') {
			steps {
				
					sh 'docker build -t frontend-app .'
				
			} 
		}
    stage('Test') {
      steps {
			
				sh 'docker container run --rm -p 8001:8080 --name node -d frontend-app' 
				sh 'sleep 5'
				sh 'curl -I http://localhost:8001'
			
		}
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push frontend-app:latest'
					} 
				}
			} 
		}
	}
}
