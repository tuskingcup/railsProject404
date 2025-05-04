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
                    -t registry-1.docker.io/tuskungg/static-web-example \
                    -t registry-1.docker.io/tuskungg/static-web-example:${env.BUILD_NUMBER} \
                    .
                """
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh """
			echo $DOCKER_USERNAME
   			echo $DOCKER_PASSWORD
			docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD registry-1.docker.io
   			docker push registry-1.docker.io/tuskungg/static-web-example:${env.BUILD_NUMBER}
		"""
                }
            }

        }
	stage('Deploy to server') {
            steps {
                script {
                    sshagent (credentials: ["SSH_KEY_DEV_SERVER"]){
                        withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            sh """
                                ssh -o StrictHostKeyChecking=no -l ubuntu 10.11.0.211 \"
                                    ls -l
                                    docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD registry-1.docker.io
                                    docker pull registry-1.docker.io/tuskungg/static-web-example:${env.BUILD_NUMBER}
                                    docker run -dp 7002:80 --name tuskungg registry-1.docker.io/tuskungg/static-web-example:${env.BUILD_NUMBER}
                                \"
                            """
                        }
                    }
                }
            }
        }


    }
}
