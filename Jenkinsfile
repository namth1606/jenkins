pipeline {
  agent any

  stages {
    stage('Stop and Cleanup Existing Image') {
      steps {
        sh 'echo Stopping and removing existing image...'
        sshagent(credentials: ['jenkins']) {
          sh 'ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 docker rm -f wego-be'
        }
      }
    }

    stage('Run New Image') {
      steps {
        sshagent(credentials: ['jenkins']) {
          sh 'ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 docker run --name wego-be -d -p 8080:80 hoainam1606/we-be:1.0.20230903035453'
        }
      }
    }
  }
  post {
    success {
      sh 'echo Image deployment successful!'
    }
    failure {
      sh 'echo Image deployment failed! Check logs for details.'
    }
  }
}
