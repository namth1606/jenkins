pipeline {
  agent any

  stages {
    stage('Stop and Cleanup Existing Image') {
      steps {
        sh 'echo Stopping and removing existing image...'
        sshagent(credentials: ['jenkins']) {
          sh '''
            ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
            docker stop wego-be || echo "No wego-be container found"
            docker rm wego-be || echo "No wego-be container found"
          '''
        }
      }
    }

    stage('Run New Image') {
      steps {
        sh 'echo Pulling latest image...'
        sshagent(credentials: ['jenkins']) {
          sh '''
            ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
            docker pull hoainam1606/we-be:1.0.20230903035453 || exit 1
          '''
        }
        sh 'echo Starting new image...'
        sshagent(credentials: ['jenkins']) {
          sh '''
            ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
            docker run --name wego-be -d -p 8080:80 hoainam1606/we-be:1.0.20230903035453 || exit 1
          '''
        }
      }
    }

    stage('Verify Image Startup') {
      steps {
        sh 'echo Checking image status...'
        sshagent(credentials: ['jenkins']) {
          sh '''
            ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
            docker logs wego-be || echo "Could not find logs for wego-be container"
          '''
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
