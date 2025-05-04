pipeline {
  agent any

  environment {
    MY_VARIABLE = "Hello, World!"
  }

    stage('Build Docker Image') {
      steps {
        sh """
          docker build --rm \
          -f Dockerfile \
          -t tuskungg/tuskungg404-service \
          -t tuskungg/tuskungg404-service:${env.BUILD_NUMBER} \
          .
        """
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying...'
      }
    }
  

  post {
    success {
      echo 'Pipeline executed successfully!'
    }

    failure {
      echo 'Pipeline execution failed!'
    }
  }
}
