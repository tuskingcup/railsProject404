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
                    -t static-web \
                    -t static-web:v1 \
                    .
                """
            }
        }
    }
}
