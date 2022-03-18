pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build') {
			steps {
					sh 'docker build -t jenkins_frontend .'
				}
		}
    stage('Test') {
      steps {
			
				sh 'docker container run --rm -p 8001:8080 --name node -d jenkins_frontend' 
				sh 'sleep 5'
				sh 'curl -I http://localhost:8001'
			
		} 
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push jenkins_frontend:latest'
					} 
				}
			} 
		}
	}
}
