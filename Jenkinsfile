// Jenkinsfile-Integration
pipeline {
    agent any
    stages {
        stage('list file') {
            steps { 
                sh 'ls -l'
                sh 'ls -l'

            }
        }
        stage('Build Docker Image') {
            steps {
                // สร้าง Docker image
                sh """
                    docker build --rm \
                    -f Dockerfile \
                    -t tuskungg/tuskungg404-service \
                    -t tuskungg/tuskungg404-service:${env.BUILD_NUMBER} \
                    .
                """
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh """
			docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD registry.hub.docker.com
   			docker push tuskungg/tuskungg404-service:${env.BUILD_NUMBER}
		"""
                }
            }

        }

    }
}
